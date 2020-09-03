## Events 

[Code Sandbox](https://codesandbox.io/s/events-95ok7)

it is convention to have event handlers defined as methods on the Component class

```javascript
class Converter extends React.Component {
    handleChangeCurrency = event => {
        this.setState({ currency: this.state.currency === '€' ? '$' : '€'})
    }
}
```

all handlers recieve an event object that adheres to the [W3C UI Events Spec](https://www.w3.org/TR/uievents/)

if using class components you must bind methods since the methods of ES6 classes are not bound by default. meaning that `this` is not defined (until binding is done). if defining methods using arrow functions, `this` is defined by default. 

 - bind manually in the constructor:
```javascript
class Converter extends React.Component {
    constructor(props) {
        super(props)
        this.handleClick = this.handleClick.bind(this)
    }
    handleClick(e) {}
}
```

 - functional method:
```javascript
class Converter extends React.Component {
    handleClick = e => {
        /*...*/
    }
    // ...
}
```

### events reference

#### clipboard
 - onCopy
 - onCut
 - onPaste

#### composition
 - onCompositionEnd
 - onCompositionStart
 - onCompositionUpdate

#### keyboard
 - onKeyDown
 - onKeyUp
 - onKeyPress

#### focus
 - onFocus
 - onBlur

#### form
 - onChange
 - onInput 
 - onSubmit

#### mouse
 - onClick
 - onContextMenu
 - onDoubleClick
 - onDrag
 - onDragEnd
 - onDragEnter
 - onDragExit
 - onDragLeave
 - onDragOver
 - onDragStart
 - onDrop
 - onMouseDown
 - onMouseEnter
 - onMoseLeave
 - onMouseMove
 - onMouseOut
 - onMouseOver
 - onMouseUp

#### selection
 - onSelect

#### touch
 - onTouchCancel
 - onTouchEnd
 - onTouchMove
 - onTouchStart

#### ui 
 - onScroll

#### mouse wheel
 - onWheel

#### media
 - onAbort
 - onCanPlay
 - onCanPlayThrough
 - onDurationChange
 - onEmptied
 - onEncrypted
 - onEnded
 - onError
 - onLoadData
 - onLoadedMetadata
 - onLoadStart
 - onPause
 - onPlay 
 - onPlaying 
 - onProgress
 - onRateChange
 - onSeeking
 - onStalled
 - onSuspend
 - onTimeUpdate
 - onVolumeChange
 - onWaiting

#### image 
 - onLoad
 - onError 
  
#### animation
 - onAnimationStart
 - onAnimationEnd
 - onAnimationIteration

#### transition
 - onTransitionEnd


### lifecycle events 

react class components can have hooks for several lifecycle events. during a lifetime of a component, there is a series of events that gets called and, to each event, you can hook and provide custom functionality. 

there are __three__ phases in a react component lifecycle:
 - mounting
 - updating
 - unmounting

__mounting__
 - when mouting, there are __four__ lifecycle methods before the component is mounted to the DOM:
  - `constructor` - called first, usually used to setup the initial state (`this.state = ...`)
  - `getDerivedStatefromProps` - used to update the state based on the props value
  - `render` - returns the JSX that builds the component interface
  - `componentDidMount` - used to perform API calls or process operations on the DOM   

__updating__
 - when updating, there are __five__ lifecycle methods before the component is mounted to the DOM:
  - `getDerivedStatefromProps` - used to update the state based on the props value
  - `shouldComponentUpdate` - returns a boolean, method is used to tell react if it should go on with rerendering. defaults to `true`, can return `false` when rerender is expensive & more control needed
  - `render` - returns the JSX that builds the component interface
  - `getSnapshotBeforeUpdate` - this method provides access to the props and state of the previous render and of the current render 
  - `componentDidUpdate` - this method is called when the component has been updated in the DOM, it is used to trigger 3rd party DOM API or call APIs that must be updated when DOM changes

__unmounting__
  - `componentWillUnmount` - this method is called when the component is removed from the DOM, can be used to perform cleanup 