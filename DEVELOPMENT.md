# Glitch Client Development Guide

This guide is for developers who want to understand, explore, and potentially work with the Glitch Flash client codebase. Whether you're studying MMO client architecture, learning ActionScript, or building something inspired by Glitch, this document will help you navigate the codebase effectively.

## 🏗️ Development Environment Setup

### Flash/ActionScript Development

The Glitch client was built using **ActionScript 3** and **Flash Professional**. To work with this codebase:

#### **Required Tools**
- **Adobe Flash Professional CS5+** or **Adobe Flash Builder 4+**
- **ActionScript 3** compiler (included with Flash tools)
- **Flash Player 11+** for testing and execution
- **Web browser** with Flash Player plugin for deployment

#### **Alternative Tools**
- **Apache Flex SDK** (free, open-source ActionScript compiler)
- **FlashDevelop** (free IDE for ActionScript development)
- **IntelliJ IDEA** with ActionScript plugin
- **VSCode** with ActionScript extensions

#### **Setup Steps**
1. Install Flash development environment of choice
2. Configure ActionScript 3 compiler settings
3. Set up project structure with proper source paths
4. Configure library paths for third-party components

### Project Configuration

#### **Compiler Settings**
```xml
<!-- Example Flash project configuration -->
<flex-config>
    <target-player>11.1</target-player>
    <source-path>com/</source-path>
    <source-path>locodeco/lib/src/</source-path>
    <library-path>locodeco/swf/libs/</library-path>
</flex-config>
```

#### **Build Process**
The client consists of multiple SWF files that can be built independently:
- **Main Application**: `BootStrap.as` → `bootstrap.swf`
- **Game Engine**: `Engine.as` → `engine.swf`
- **Utility Tools**: Individual tools like `ItemViewer.as`, `Vanity.as`
- **Asset Libraries**: Various FLA files in `TSEngineAssets/`

## 📖 Codebase Navigation Guide

### Understanding the Architecture

#### **Bootstrap Flow**
```actionscript
BootStrap.as 
    → FlashVarModel (config from web page)
    → StageBeacon.init() (global stage access)
    → BootStrapController.init() (application startup)
    → Engine loading and initialization
```

#### **Engine Initialization**
```actionscript
Engine.as
    → MainEngineController() (primary game controller)
    → NetController() (network communication)
    → Various view controllers and models
```

#### **Message Flow**
```actionscript
Player Action → UI Component → Controller → NetOutgoing Message → Server
Server Response → NetIncoming Message → Controller → Model Update → View Refresh
```

### Key Code Patterns

#### **Include System**
ActionScript uses `#include` directives for code organization:
```actionscript
//#include include/takeable.js
//#include include/food.js
```
*These are processed at compile time, similar to C preprocessor directives.*

#### **Event-Driven Architecture**
Most systems use Flash's event system:
```actionscript
// Dispatching events
dispatchEvent(new TSEvent(TSEvent.CHANGED, {item: item}));

// Listening for events  
addEventListener(TSEvent.CHANGED, onItemChanged);
```

#### **Singleton Pattern**
Many managers use singletons for global access:
```actionscript
public static function get instance():AssetManager {
    if (!_instance) _instance = new AssetManager();
    return _instance;
}
```

## 🔍 Core Systems Deep Dive

### Network Communication System

#### **Architecture Overview**
The networking system handles all client-server communication through a socket-based protocol:

```
Client Action → NetOutgoing VO → NetController → Socket → Server
Server Response → Socket → NetIncoming VO → Message Handler → Model Update
```

#### **Key Classes**
- **`NetController.as`**: Main network management and message routing
- **`NetDelegateSocket.as`**: Low-level socket communication wrapper
- **`NetOutgoing*VO.as`**: Value objects for client-to-server messages
- **`NetIncoming*VO.as`**: Value objects for server-to-client messages

#### **Message Types**
Explore these key message categories:
```actionscript
// Movement messages
NetOutgoingMoveXYVO, NetOutgoingMoveVecVO

// Item interaction  
NetOutgoingItemstackVerbVO, NetOutgoingItemstackMenuVO

// Chat and social
NetOutgoingLocalChatVO, NetOutgoingImSendVO

// Trading and economy
NetOutgoingTradeStartVO, NetOutgoingStoreBuyVO
```

#### **Connection Management**
```actionscript
// Connection testing and diagnostics
ConnectionTest.as - Comprehensive network testing utility
    → Socket policy testing
    → Server connectivity validation  
    → Firewall detection
    → Local storage verification
```

### Avatar and Character System

#### **Avatar Rendering Pipeline**
```actionscript
AvatarView.as
    → Character data (PC object)
    → Asset loading (clothing, faces, animations)
    → Multi-layer rendering (base, clothing, accessories)
    → Animation state management
    → Performance optimization
```

#### **Customization System**
```actionscript
Vanity.as / VanityMirror.as
    → Facial feature selection and positioning
    → Clothing and color customization
    → Real-time preview rendering
    → Save/load avatar configurations
```

#### **Key Files to Explore**
- **`AvatarView.as`**: Core avatar rendering and animation
- **`PCView.as`**: Player character view management
- **`AbstractAvatarView.as`**: Base avatar functionality
- **`VanityMirror.as`**: Character customization interface
- **`AvatarDisplayer2011.as`**: Avatar testing and preview tool

### Asset Management System

#### **Dynamic Loading Architecture**
```actionscript
AssetManager.as
    → Asset request queue
    → SWF/image loading
    → Caching and memory management
    → Asset resolution and fallbacks
```

#### **Asset Types**
- **SWF Files**: Character animations, UI components, world objects
- **Images**: Textures, backgrounds, interface graphics
- **Sounds**: Music, effects, ambient audio
- **Data**: Configuration files, localization, game data

#### **Loading Strategy**
```actionscript
// Lazy loading pattern
if (!assetLoaded(assetId)) {
    loadAsset(assetId, onAssetComplete);
} else {
    useAsset(getAsset(assetId));
}
```

### User Interface Framework

#### **UI Component Hierarchy**
```actionscript
AbstractTSView (base view)
    → TSMainView (main game interface)
        → Various dialog and panel components
        → Chat interface components
        → Inventory and trading interfaces
```

#### **Key UI Classes**
- **`TSMainView.as`**: Primary game interface container
- **`AbstractTSView.as`**: Base class for all UI components
- **`IFocusableComponent.as`**: Interface for focusable UI elements
- **`TabbedPaneTab.as`**: Tab interface components

#### **Chat System Deep Dive**
```actionscript
com/tinyspeck/engine/view/ui/chat/
    → ChatArea.as (main chat display)
    → ChatInput.as (message input)
    → ChatChannel.as (channel management)
    → LocalChatView.as (location-based chat)
```

## 🛠️ Development Tools and Utilities

### Built-in Debug Tools

#### **Connection Testing** (`ConnectionTest.as`)
Comprehensive network diagnostics tool:
```actionscript
// Test server connectivity
test_connection(host, port, token)

// Validate local storage
test_lso(crossdomain_url) 

// Check crossdomain policy
test_crossdomain(url)
```

*Usage*: Compile and run this tool to diagnose network issues and validate client-server communication setup.

#### **Item Database Browser** (`ItemViewer.as`)
Tool for exploring all game items:
```actionscript
// Browse item database
// View item properties and assets
// Test item interactions
// Validate item graphics and animations
```

*Significance*: Essential for understanding the massive item system that made Glitch unique, with over 1,000 interactive items.

#### **Avatar Customization Tool** (`Vanity.as`)
Character appearance testing utility:
```actionscript
// Test all avatar combinations
// Preview clothing and accessories
// Validate character rendering
// Export avatar configurations
```

#### **Administrative Tools** (`GodItemViewer.as`)
Developer/admin interface for content management:
```actionscript
// Administrative item manipulation
// Content testing and validation
// Debug mode functionality
// Developer-only features
```

### External Development Tools

#### **ActionScript Development**
- **FlashDevelop**: Free, powerful ActionScript IDE
- **IntelliJ IDEA**: Professional IDE with ActionScript support
- **VSCode**: Lightweight editor with ActionScript extensions

#### **Asset Tools**
- **Flash Professional**: For editing FLA files and animations
- **Adobe After Effects**: For complex animations
- **Photoshop**: For image asset creation and editing

#### **Debugging and Profiling**
- **Flash Player Debugger**: Runtime debugging and profiling
- **Adobe Scout**: Performance profiling for Flash applications
- **Monster Debugger**: Advanced debugging tool for ActionScript

## 🔬 Code Exploration Strategies

### Starting Points for Different Interests

#### **Network Programming**
1. Start with `ConnectionTest.as` to understand the connection flow
2. Explore `NetController.as` for message handling architecture
3. Study `NetOutgoing*VO.as` classes to see client-server communication
4. Look at `NetDelegateSocket.as` for low-level socket management

#### **User Interface Development**
1. Begin with `TSMainView.as` for overall UI architecture
2. Explore `AbstractTSView.as` for base UI component patterns
3. Study chat system in `com/tinyspeck/engine/view/ui/chat/`
4. Examine specific dialogs and panels for interaction patterns

#### **Game Client Architecture**
1. Start with `BootStrap.as` and `Engine.as` for application lifecycle
2. Study `MainEngineController.as` for core game management
3. Explore `WorldModel.as` and `StateModel.as` for state management
4. Look at `AssetManager.as` for content loading strategies

#### **Avatar and Animation Systems**
1. Begin with `AvatarView.as` for character rendering
2. Study `Vanity.as` for customization interface
3. Explore animation systems in `com/tinyspeck/engine/animatedbitmap/`
4. Look at avatar data structures in engine models

### Search Strategies

#### **Finding Specific Features**
```bash
# Search for network message types
grep -r "NetOutgoing" com/tinyspeck/engine/net/

# Find UI components
find com/tinyspeck/engine/view/ui/ -name "*.as"

# Locate avatar-related code
grep -r "avatar\|Avatar" com/tinyspeck/

# Find asset loading code
grep -r "AssetManager\|loadAsset" com/tinyspeck/
```

#### **Understanding Data Flow**
```bash
# Trace message handling
grep -r "processMessage\|handleMessage" com/tinyspeck/

# Find event dispatching
grep -r "dispatchEvent\|addEventListener" com/tinyspeck/

# Locate model updates
grep -r "updateModel\|modelUpdate" com/tinyspeck/
```

## 🧪 Testing and Experimentation

### Setting Up Test Environment

#### **Flash Player Configuration**
- Enable Flash Player Debugger for runtime debugging
- Configure trust settings for local file access
- Set up logging and trace output capture

#### **Web Server Setup**
For testing in browser environment:
```html
<!-- Basic HTML wrapper -->
<object type="application/x-shockwave-flash" data="bootstrap.swf">
    <param name="flashvars" value="host=localhost&port=1001" />
    <param name="allowScriptAccess" value="always" />
</object>
```

### Experimentation Ideas

#### **Network Protocol Analysis**
- Use `ConnectionTest.as` to understand connection requirements
- Modify `NetOutgoing*VO` classes to log message contents
- Implement mock server responses for testing

#### **UI Component Development**
- Create custom UI components based on existing patterns
- Modify existing interfaces to understand component architecture
- Test responsive design patterns used in the client

#### **Asset System Exploration**
- Create custom asset loading scenarios
- Test asset caching and memory management
- Explore dynamic content loading patterns

## 📚 Understanding Third-Party Dependencies

### Major Libraries Used

#### **Animation and Tweening**
- **Tweener** (`caurina/transitions`): Sophisticated animation library
- **GreenSock** (`com/greensock`): Professional animation framework

#### **Utilities and Components**
- **Bit101** (`com/bit101`): UI component library
- **Adobe Utils** (`com/adobe`): Encoding, JSON, and utility functions

#### **Graphics and Effects**
- **Quasimondo** (`com/quasimondo`): Image processing and effects
- **Object Pool** (`de/polygonal`): Memory management and optimization

### Library Integration Patterns

#### **Tweening System**
```actionscript
// Using Tweener for animations
Tweener.addTween(target, {x: 100, time: 1.0, ease: "easeOutCubic"});

// GreenSock integration
TweenLite.to(target, 1.0, {x: 100, ease: Cubic.easeOut});
```

#### **Component Libraries**
```actionscript
// Bit101 components
var button:PushButton = new PushButton(parent, x, y, "Click Me");

// Custom component wrapping
class TSButton extends PushButton {
    // Glitch-specific enhancements
}
```

## 🎯 Common Development Tasks

### Adding New UI Components

#### **Component Creation Pattern**
```actionscript
// 1. Extend base view class
class MyNewDialog extends AbstractTSView {
    
    // 2. Implement required methods
    override protected function init():void {
        super.init();
        // Component initialization
    }
    
    // 3. Handle user interactions
    private function onButtonClick(event:MouseEvent):void {
        // Handle user actions
    }
    
    // 4. Communicate with controllers
    private function sendToServer():void {
        var msg:NetOutgoingGenericMsgVO = new NetOutgoingGenericMsgVO();
        // Send message to server
    }
}
```

### Extending the Asset System

#### **Custom Asset Loading**
```actionscript
// 1. Register new asset types
AssetManager.instance.registerAssetType("custom", CustomAssetLoader);

// 2. Implement custom loader
class CustomAssetLoader extends AssetLoader {
    override protected function loadAsset():void {
        // Custom loading logic
    }
}

// 3. Use new asset type
AssetManager.instance.loadAsset("custom_asset", onAssetLoaded);
```

### Network Message Development

#### **Creating New Messages**
```actionscript
// 1. Define outgoing message
class NetOutgoingCustomActionVO extends NetOutgoingMessageVO {
    public var action_data:Object;
    
    public function NetOutgoingCustomActionVO(data:Object) {
        super(MessageTypes.CUSTOM_ACTION);
        this.action_data = data;
    }
}

// 2. Handle in controller
NetController.instance.sendMessage(new NetOutgoingCustomActionVO(data));

// 3. Process incoming response
private function handleCustomResponse(msg:NetIncomingMessageVO):void {
    // Process server response
}
```

## 🐛 Debugging and Troubleshooting

### Common Issues and Solutions

#### **Flash Player Compatibility**
- **Issue**: Code doesn't run in modern browsers
- **Solution**: Use Flash Player Projector or AIR runtime for testing

#### **Cross-Domain Security**
- **Issue**: Assets fail to load due to security restrictions
- **Solution**: Configure crossdomain.xml policy files

#### **Memory Management**
- **Issue**: Application becomes slow over time
- **Solution**: Implement proper object disposal and event listener cleanup

### Debugging Techniques

#### **Trace Debugging**
```actionscript
// Add strategic trace statements
trace("Network message sent:", msg.type, msg.data);

// Use conditional tracing
CONFIG::debug {
    trace("Debug info:", debugData);
}
```

#### **Visual Debugging**
```actionscript
// Show bounding boxes
graphics.lineStyle(1, 0xFF0000);
graphics.drawRect(bounds.x, bounds.y, bounds.width, bounds.height);

// Display debug information
var debugText:TextField = new TextField();
debugText.text = "Debug: " + debugInfo;
addChild(debugText);
```

## 🚀 Advanced Topics

### Performance Optimization

#### **Memory Management**
- Implement object pooling for frequently created objects
- Use weak references where appropriate
- Dispose of event listeners and graphics objects properly

#### **Rendering Optimization**
- Use bitmap caching for static content
- Implement efficient display list management
- Optimize asset loading and caching strategies

### Architecture Patterns

#### **Model-View-Controller**
The client uses MVC architecture extensively:
- **Models**: Data representation and business logic
- **Views**: User interface and presentation
- **Controllers**: User input handling and coordination

#### **Event-Driven Communication**
All system communication uses Flash's event system:
- Loose coupling between components
- Centralized event handling through StageBeacon
- Type-safe event objects with custom data

#### **Command Pattern**
User actions are processed through command objects:
- Encapsulation of user actions
- Undo/redo functionality support
- Network message generation from commands

## 📈 Next Steps

### For Learning
1. **Start Small**: Begin with utility tools like `ItemViewer.as`
2. **Follow Data Flow**: Trace how user actions become network messages
3. **Experiment**: Modify existing components to understand behavior
4. **Document**: Keep notes on architectural patterns you discover

### For Development
1. **Modern Migration**: Consider porting patterns to modern web technologies
2. **Component Extraction**: Extract reusable patterns for new projects
3. **Architecture Study**: Use as reference for client-server game architecture
4. **Educational Use**: Create tutorials and guides for others

### For Research
1. **Virtual World Design**: Study social interaction patterns
2. **UI/UX Analysis**: Examine interface design for complex applications
3. **Performance Study**: Analyze optimization techniques for real-time applications
4. **Architecture Documentation**: Create detailed technical documentation

---

*This development guide provides the foundation for understanding and working with the Glitch client codebase. The client represents a sophisticated example of Flash/ActionScript architecture and provides valuable insights into MMO client development, regardless of the target platform.*