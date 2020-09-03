## Firegram

### tutorial:

https://www.youtube.com/watch?v=vUe91uOx7R0&t=171s

### starter code:

https://github.com/iamshaunjp/firegram/tree/starter-files

### local project path:

/home/tim/Projects/React/firegram

### my repo:

https://github.com/tim-corley/firegram

**NOTE:** to clone just the `starter-files` branch, use:

```bash
➜  React git clone -b starter-files --single-branch https://github.com/iamshaunjp/firegram.git
```

`git clone -b <branch-name> --single-branch <repo url>`

1. **setup & run**

```bash
➜  React cd firegram
➜  firegram git:(starter-files) ls
package.json  package-lock.json  public  README.md  src
➜  firegram git:(starter-files) code .
➜  firegram git:(starter-files) npm install
➜  firegram git:(starter-files) npm start
```

2. **firebase setup**

- firebase = "backend as a service"

a) add new project at [firebase console](https://console.firebase.google.com/)

b) from [project dashboard](https://console.firebase.google.com/project/firegram-3b755/overview) add new web app

c) grab the firebase sdk config snipper via: **Settings > General > Your Apps > Config**

d) add snippet to project

```bash
➜  src git:(starter-files) ✗ mkdir firebase && cd $_ && touch config.js
➜  firebase git:(starter-files) ✗ nano config.js
```

e) install firebase within project

```bash
➜  firegram git:(starter-files) ✗ npm install firebase
```

f) add firebase import (along w/ storage & firestore) to config file

```javascript
// config.js
import * as firebase from "firebase/app";
import "firebase/storage";
import "firebase/firestore";

// web app's firebase configuration
const firebaseConfig = {
  apiKey: "AIzaSyDyUHKFFqoFB5pc_BwGQwP23-C44p8VC4w",
  authDomain: "firegram-3b755.firebaseapp.com",
  databaseURL: "https://firegram-3b755.firebaseio.com",
  projectId: "firegram-3b755",
  storageBucket: "firegram-3b755.appspot.com",
  messagingSenderId: "218576518980",
  appId: "1:218576518980:web:a078eeff751da2b757a111",
};

// intialize firebase app
firebase.initializeApp(firebaseConfig);

// initialize storage & firestore
const projectStorage = firebase.storage();
const projectFirestore = firebase.firestore();

export { projectStorage, projectFirestore };
```

g) setup storage & firestore via firebase console

- be sure, with storage, after creating bucket - go to rules ans remove `if request.auth != null` so that we can easily add items during development

3. **upload form**

```javascript
// src/comps/UploadForm.js
import React, { useState } from "react";

const UploadForm = () => {
  const [file, setFile] = useState(null);
  const [error, setError] = useState(null);

  const allowedTypes = ["image/png", "image/jpeg"];

  const changeHandler = (e) => {
    let selected = e.target.files[0];

    if (selected && allowedTypes.includes(selected.type)) {
      setFile(selected);
      setError("");
    } else {
      setFile(null);
      setError("Please select a valid image file (.png or .jpg) for upload.");
    }
  };

  return (
    <form>
      <input type="file" onChange={changeHandler} />
      <div className="output">
        {error && <div className="error">{error}</div>}
        {file && <div>{file.name}</div>}
      </div>
    </form>
  );
};

export default UploadForm;
```

4. **firebase storage custom hook**

```javascript
// useStore.js
import { useState, useEffect } from "react";
import { projectStorage } from "../firebase/config";

// custom hook
const useStorage = (file) => {
  const [progress, setProgress] = useState(0);
  const [error, setError] = useState(null);
  const [url, setUrl] = useState(null);

  useEffect(() => {
    const storageRef = projectStorage.ref(file.name);

    storageRef.put(file).on(
      "state_changed",
      (snap) => {
        let percentage = (snap.bytesTransferred / snap.totalBytes) * 100;
        setProgress(percentage);
      },
      (err) => {
        setError(err);
      },
      async () => {
        const url = await storageRef.getDownloadURL();
        setUrl(url);
      }
    );
  }, [file]);

  return { progress, url, error };
};

export default useStorage;
```

5. **progress bar**

```javascript
// ProgressBar.js
import React, { useEffect } from "react";
import useStorage from "../hooks/useStorage";

const ProgressBar = ({ file, setFile }) => {
  const { url, progress } = useStorage(file);

  useEffect(() => {
    if (url) {
      setFile(null);
    }
  }, [url, setFile]);

  return <div className="progress-bar" style={{ width: progress + "%" }}></div>;
};

export default ProgressBar;
```

6. **add storage url to firestore db**

```javascript
// useStorage.js
import { useState, useEffect } from "react";
import {
  projectStorage,
  projectFirestore,
  timestamp,
} from "../firebase/config";

// custom hook
const useStorage = (file) => {
  const [progress, setProgress] = useState(0);
  const [error, setError] = useState(null);
  const [url, setUrl] = useState(null);

  useEffect(() => {
    // references
    const storageRef = projectStorage.ref(file.name);
    const collectionRef = projectFirestore.collection("images");

    storageRef.put(file).on(
      "state_changed",
      (snap) => {
        let percentage = (snap.bytesTransferred / snap.totalBytes) * 100;
        setProgress(percentage);
      },
      (err) => {
        setError(err);
      },
      async () => {
        const url = await storageRef.getDownloadURL();
        const createdAt = timestamp();
        collectionRef.add({ url, createdAt });
        setUrl(url);
      }
    );
  }, [file]);

  return { progress, url, error };
};

export default useStorage;
```

- be sure to add the timestamp fieldvalue in `config.js`

```javascript
// config.js
//...
// initialize storage & firestore
const projectStorage = firebase.storage();
const projectFirestore = firebase.firestore();
const timestamp = firebase.firestore.FieldValue.serverTimestamp;

export { projectStorage, projectFirestore, timestamp };
```

7. **firestore custom hook & ImageGrid hookup**

used to listen to the db and refresh the app when changes made

```javascript
// useFirestore.js
import { useState, useEffect } from "react";
import { projectFirestore } from "../firebase/config";

const useFirestore = (collection) => {
  const [docs, setDocs] = useState([]);

  useEffect(() => {
    const unsub = projectFirestore
      .collection(collection)
      .orderBy("createdAt", "desc")
      .onSnapshot((snap) => {
        let documents = [];
        snap.forEach((doc) => {
          documents.push({ ...doc.data(), id: doc.id });
        });
        setDocs(documents);
      });
    return () => unsub();
  }, [collection]);
  return { docs };
};

export default useFirestore;
```

```javascript
// ImageGrid.js
import React from "react";
import useFirestore from "../hooks/useFirestore";

const ImageGrid = () => {
  const { docs } = useFirestore("images");

  return (
    <div className="img-grid">
      {docs &&
        docs.map((doc) => (
          <div className="img-wrap" key={doc.id}>
            <img src={doc.url} alt="" />
          </div>
        ))}
    </div>
  );
};

export default ImageGrid;
```

8. **image modal**

- allow access to state (at root)

```javascript
// App.js
import React, { useState } from "react";
import Title from "./comps/Title";
import UploadForm from "./comps/UploadForm";
import ImageGrid from "./comps/ImageGrid";
import Modal from "./comps/Modal";

function App() {
  const [selectedImg, setSelectedImg] = useState(null);

  return (
    <div className="App">
      <Title />
      <UploadForm />
      <ImageGrid setSelectedImg={setSelectedImg} />
      {selectedImg && (
        <Modal selectedImg={selectedImg} setSelectedImg={setSelectedImg} />
      )}
    </div>
  );
}

export default App;
```

- create modal component

```javascript
import React from "react";

const Modal = ({ selectedImg, setSelectedImg }) => {
  const handleClick = (e) => {
    if (e.target.classList.contains("backdrop")) {
      setSelectedImg(null);
    }
  };

  return (
    <div className="backdrop" onClick={handleClick}>
      <img src={selectedImg} alt="zoomed" />
    </div>
  );
};

export default Modal;
```

9. **add animation**

using [Framer Motion](https://www.framer.com/motion/)

- install framer motion

```bash
➜  firegram git:(starter-files) npm i framer-motion --save-dev
```

- import & using within component by prepending 'motion' to desired tag(s) and adding motion attributes

```javascrip
import React from "react";
import useFirestore from "../hooks/useFirestore";
import { motion } from "framer-motion";

const ImageGrid = ({ setSelectedImg }) => {
  const { docs } = useFirestore("images");

  return (
    <div className="img-grid">
      {docs &&
        docs.map((doc) => (
          <motion.div
            className="img-wrap"
            key={doc.id}
            layout
            whileHover={{ opacity: 1 }}
            onClick={() => setSelectedImg(doc.url)}
          >
            <motion.img
              src={doc.url}
              alt=""
              initial={{ opacity: 0 }}
              animate={{ opacity: 1 }}
              transition={{ delay: 1 }}
            />
          </motion.div>
        ))}
    </div>
  );
};

export default ImageGrid;
```

### devops

- create repo ([github cli](https://cli.github.com/manual/gh_repo_create)):

```bash
➜  firegram git:(starter-files) gh repo create -d "an instagram inspired web app to host photos"

```

- update / change remote:

```bash
➜  firegram git:(starter-files) git remote set-url origin git@github.com:tim-corley/firegram.git
```

- create a master branch

```bash
  ➜  firegram git:(starter-files) git checkout -b master
```

- push

```bash
➜  filegram git:(master) git push -u origin master
```

- to deploy on firebase ([firebase cli]()):

```
firebase login
firebase init
firebase deploy
```
