# Glitch Flash Client

> **The complete client-side codebase for Glitch, the beloved browser-based MMO that ran from 2009-2012**

This repository contains the entire Flash/ActionScript 3 client that powered [Glitch](http://glitchthegame.com), one of the most innovative and creative MMOs ever created. Developed by Tiny Speck (who later created Slack), this client handled all player interaction, rendering, and communication with the game server for a world where hundreds of thousands of players explored, crafted, socialized, and embarked on whimsical adventures.

## 🌟 What Makes This Client Special

This isn't just any game client - it's a **complete MMO client implementation** showcasing advanced Flash/ActionScript architecture:

- **Sophisticated Real-time Communication** with robust socket-based server connectivity
- **Advanced Avatar System** with complex character customization and animation
- **Rich UI Framework** supporting complex game interfaces, chat, trading, and social features  
- **Comprehensive Asset Management** handling thousands of game assets, animations, and sounds
- **Powerful Debug Tools** including connection testing, item viewers, and administrative interfaces
- **Location Decoration System** (locodeco) for building and customizing game environments
- **Performance Optimization** with memory management, object pooling, and efficient rendering

## 🎮 Client-Server Ecosystem

This client works in tandem with the **[glitch-GameServerJS](https://github.com/ap0ught/glitch-GameServerJS)** repository to create the complete Glitch experience:

### **Client Responsibilities** (This Repository)
- **User Interface**: All player interaction, menus, dialogs, and HUD elements
- **Rendering Engine**: Graphics, animations, effects, and visual presentation
- **Input Management**: Keyboard, mouse, and touch input processing
- **Asset Loading**: Dynamic loading of graphics, sounds, and game content
- **Network Communication**: Socket-based messaging with the game server
- **Local State**: Client-side caching, preferences, and temporary data

### **Server Responsibilities** ([glitch-GameServerJS](https://github.com/ap0ught/glitch-GameServerJS))
- **Game Logic**: All authoritative game rules, physics, and state management
- **Player Data**: Character progression, inventory, achievements, and statistics  
- **World State**: Location data, item placement, and environmental changes
- **Social Systems**: Chat, groups, trading, and player interactions
- **Content Management**: Quests, NPCs, items, and dynamic events

### **Communication Protocol**
The client and server communicate through a sophisticated message-passing system:
- **NetOutgoing*** classes send player actions to server
- **NetIncoming*** classes receive server updates and responses
- **Real-time Updates** for movement, chat, and world changes
- **Reliable Delivery** ensuring critical game state synchronization

## 🏗️ Client Architecture

### Core Systems

#### **Bootstrap & Engine** (`BootStrap.as`, `Engine.as`)
The foundation layer that initializes the game client:
- **Security Configuration**: Cross-domain policies and permissions
- **Stage Setup**: Display properties, scaling, and focus management  
- **Error Handling**: Global error catching and reporting
- **Version Management**: Client version tracking and compatibility
- **Flash Variables**: Configuration from web page parameters

*Significance*: This bootstrap system allows the Flash client to securely load and run in any web browser while maintaining proper security boundaries and error reporting for a live MMO environment.

#### **Network Controller** (`com/tinyspeck/engine/control/engine/NetController.as`)
Manages all client-server communication:
- **Socket Management**: Connection establishment, heartbeat, and recovery
- **Message Queue**: Reliable message delivery and ordering
- **Protocol Handling**: Serialization/deserialization of game messages
- **Connection Testing**: Network diagnostics and firewall detection

*Significance*: This robust networking layer enables real-time multiplayer gameplay over unreliable internet connections, handling everything from player movement to complex trading interactions.

#### **Asset Management** (`com/tinyspeck/engine/port/AssetManager`)
Dynamic loading and caching of game content:
- **SWF Loading**: Animation files, character assets, and UI components
- **Image Management**: Textures, backgrounds, and visual effects
- **Sound System**: Music, sound effects, and ambient audio  
- **Caching Strategy**: Memory management for thousands of assets

*Significance*: This system allows Glitch to have a massive, detailed world without requiring huge initial downloads, loading content dynamically as players explore.

#### **Avatar System** (`com/tinyspeck/engine/view/AvatarView.as`)
Complete character representation and customization:
- **Character Rendering**: Complex multi-layer avatar display
- **Customization Engine**: Faces, clothing, colors, and accessories
- **Animation System**: Movement, emotes, and action animations
- **Physics Integration**: Collision detection and movement constraints

*Significance*: This sophisticated avatar system enabled Glitch's unique character customization where every player could create a truly unique appearance, contributing to the game's strong sense of personal identity.

### User Interface Framework

#### **Main View System** (`com/tinyspeck/engine/view/TSMainView.as`)
The primary game interface manager:
- **Window Management**: Overlay dialogs, panels, and UI components
- **Input Routing**: Keyboard shortcuts and mouse event handling
- **Layout Management**: Responsive interface scaling and positioning
- **Focus Management**: UI element focus and tab ordering

#### **Chat System** (`com/tinyspeck/engine/view/ui/chat/`)
Comprehensive communication interface:
- **Local Chat**: Location-based conversation with nearby players
- **Group Chat**: Private group and party communication
- **Instant Messaging**: Direct player-to-player messaging
- **Channel Management**: Multiple chat channels and filtering

*Significance*: The robust chat system was crucial to Glitch's social nature, enabling the rich community interactions that made the game special.

#### **Trading & Economy UI** (`com/tinyspeck/engine/view/ui/`)
Economic interaction interfaces:
- **Trading Windows**: Secure player-to-player item exchange
- **Shop Interfaces**: NPC vendors and player-owned stores
- **Auction System**: Complex bidding and marketplace UI
- **Inventory Management**: Sophisticated item organization and display

*Significance*: These economic interfaces supported Glitch's complex player-driven economy, enabling everything from simple trades to sophisticated market dynamics.

### Content Systems

#### **Item Stack System** (`com/tinyspeck/engine/view/itemstack/`)
Comprehensive item interaction framework:
- **Item Display**: Visual representation of all game items
- **Verb System**: Context-sensitive action menus for items
- **Drag & Drop**: Intuitive item manipulation and transfer
- **Tooltip System**: Rich information display for items

*Significance*: This system enabled Glitch's unique approach where nearly everything in the world was interactive, from simple rocks to complex crafting machines.

#### **Location Decoration (locodeco)** (`locodeco/`)
Advanced world-building and customization tools:
- **Platform Creation**: Building custom geography and structures
- **Asset Placement**: Positioning decorative and functional items
- **Physics Integration**: Collision detection for custom content
- **Export/Import**: Sharing custom locations and designs

*Significance*: The locodeco system allowed players and developers to create custom locations, enabling user-generated content and rapid world expansion.

#### **Game Overlay System** (`com/tinyspeck/engine/view/gameoverlay/`)
Rich contextual information and interaction:
- **Quest Dialogs**: Narrative conversation trees and story content
- **Tutorial System**: New player guidance and feature introduction
- **Help System**: Context-sensitive assistance and documentation
- **Notification System**: Game events, achievements, and alerts

## 🛠️ Development Tools & Utilities

### **Connection Testing** (`ConnectionTest.as`)
Comprehensive network diagnostics:
- **Server Connectivity**: Tests connection to game servers
- **Firewall Detection**: Identifies network configuration issues  
- **Socket Policy**: Validates Flash security policies
- **Local Storage**: Tests browser data storage capabilities

*Significance*: These tools enabled Tiny Speck to diagnose player connection issues in real-time, crucial for maintaining service quality in a live MMO.

### **Avatar Tools** (`AvatarDisplayer2011.as`, `Vanity.as`)
Character customization and testing utilities:
- **Avatar Preview**: Real-time character appearance testing
- **Asset Validation**: Ensuring avatar components work together
- **Color Testing**: Validating appearance across different combinations
- **Export Tools**: Generating avatar data for server storage

### **Item Viewers** (`ItemViewer.as`, `GodItemViewer.as`)
Content development and debugging tools:
- **Item Database**: Browse and test all game items
- **Asset Validation**: Ensure item graphics and animations work correctly
- **Property Editing**: Modify item properties for testing
- **God Mode Tools**: Administrative item management functions

### **Badge & Card Systems** (`BadgeMaker.as`, `UpgradeCardViewer.as`)
Achievement and progression content tools:
- **Badge Creation**: Design and preview achievement badges
- **Card System**: Imagination-based upgrade card interface
- **Visual Testing**: Ensure proper display across different scenarios

## 📁 Repository Structure

```
├── Engine.as                 # Core game engine entry point
├── BootStrap.as              # Application bootstrap and initialization
├── ConnectionTest.as         # Network diagnostics and testing
├── Vanity.as                 # Avatar customization system
├── AvatarDisplayer2011.as    # Avatar rendering and testing tools
├── ItemViewer.as             # Item database browser and testing
├── GodItemViewer.as          # Administrative item management tools
├── BadgeMaker.as             # Achievement badge creation tools
├── UpgradeCardViewer.as      # Imagination card system interface
├── LocalStorageRequester.as  # Browser storage interface
│
├── com/tinyspeck/            # Core engine and game systems
│   ├── bootstrap/            # Application startup and initialization
│   ├── bridge/               # Flash-JavaScript communication bridge
│   ├── core/                 # Shared utilities and base functionality
│   ├── debug/                # Development and debugging tools
│   ├── engine/               # Main game engine components
│   │   ├── control/          # Game controllers and logic management
│   │   ├── data/             # Data models and storage systems
│   │   ├── loader/           # Asset loading and management
│   │   ├── model/            # Game state and data models
│   │   ├── net/              # Network communication systems
│   │   ├── view/             # User interface and rendering
│   │   └── util/             # Engine utilities and helpers
│   ├── tstweener/            # Animation and tweening library
│   └── vanity/               # Avatar customization components
│
├── locodeco/                 # Location decoration and world-building
│   ├── lib/src/locodeco/     # Core locodeco functionality
│   │   ├── models/           # Location and geometry data models
│   │   └── util/             # Utility functions for world building
│   └── swf/libs/             # Required Flash libraries
│
├── TSEngineAssets/           # Game assets and resources
│   ├── src/assets/           # Raw asset files (images, sounds, fonts)
│   └── *.fla files           # Flash animation source files
│
├── assets/                   # Additional game assets and resources
├── loading/                  # Loading screen assets and animations
│
└── Third-party Libraries:
    ├── at/leichtgewicht/     # Draw library by Martin Heidegger
    ├── caurina/transitions/  # Tweener animation library
    ├── com/adobe/            # Adobe utilities (encoding, JSON, Base64)
    ├── com/bit101/           # Bit101 component library
    ├── com/greensock/        # GreenSock animation framework
    ├── com/quasimondo/       # Image processing utilities
    ├── com/quietless/        # Bitmap snapshot utilities
    ├── de/polygonal/         # Object pooling system
    ├── net/hires/            # Stats monitoring library
    └── org/bytearray/        # GIF encoding/decoding utilities
```

## 🚀 Getting Started

### Understanding the Codebase

This Flash/ActionScript 3 codebase was designed for Flash Player and requires specific tools to build and run:

#### **Development Environment**
- **Adobe Flash Professional** or **Adobe Flash Builder** for compilation
- **ActionScript 3** knowledge for code modification
- **Flash Player** for testing and execution
- **Web browser** with Flash Player plugin for deployment

#### **Key Entry Points**
1. **`BootStrap.as`** - Application startup and configuration
2. **`Engine.as`** - Core game engine initialization  
3. **`com/tinyspeck/engine/control/MainEngineController.as`** - Primary game controller
4. **Connection testing tools** for understanding network communication

### For Game Developers

This codebase provides invaluable insights into:

#### **MMO Client Architecture**
- **Real-time Communication**: Socket-based client-server messaging
- **Asset Pipeline**: Dynamic loading and caching of game content
- **UI Framework**: Complex interface management for MMO features
- **Performance Optimization**: Memory management in long-running applications

#### **Flash/ActionScript Patterns**
- **Event-Driven Architecture**: Comprehensive event handling and dispatch
- **Component-Based UI**: Reusable interface components and widgets
- **Animation Systems**: Complex character and world animations
- **Security Model**: Cross-domain policies and sandboxing

### For Researchers & Students

#### **Virtual World Studies**
- **Avatar Systems**: Digital identity and character representation
- **Social Interfaces**: Communication and community features
- **User Experience**: Interface design for complex virtual environments
- **Accessibility**: Making virtual worlds usable for diverse players

#### **Software Engineering**
- **Large-Scale Flash Applications**: Architecture patterns for complex projects
- **Client-Server Communication**: Real-time networking in games
- **Asset Management**: Handling large amounts of dynamic content
- **Cross-Platform Compatibility**: Web-based application deployment

### For Glitch Enthusiasts

#### **Discovering Hidden Features**
- **Debug Tools**: Administrative interfaces and testing utilities
- **Content Exploration**: Browse all game assets and animations
- **Avatar Customization**: Understand the full range of character options
- **World Building**: Explore the locodeco system for custom locations

## 💎 Notable Features & Innovations

### **Advanced Avatar Customization**
Glitch's avatar system was years ahead of its time:
- **Infinite Variety**: Mix and match facial features, clothing, and colors
- **Real-time Preview**: See changes instantly while customizing
- **Social Expression**: Unique appearances that reflected player personality
- **Technical Achievement**: Complex multi-layer rendering with efficient performance

### **Seamless World Integration**
The client seamlessly integrated with a massive game world:
- **Location Streaming**: Smooth transitions between game areas
- **Dynamic Content**: Real-time updates as the world changed around players
- **Performance Scaling**: Efficient rendering regardless of location complexity
- **Social Presence**: Always seeing other players and their activities

### **Rich Communication Systems**
Communication was central to Glitch's social experience:
- **Contextual Chat**: Different communication modes for different situations
- **Visual Expression**: Emotes, gestures, and visual communication
- **Persistent History**: Chat history and conversation management
- **Accessibility**: Text-based communication accessible to all players

### **Interactive World Design**
Everything in Glitch was designed to be interactive:
- **Universal Interaction**: Nearly every object in the world was clickable
- **Context Menus**: Rich action menus that changed based on player skills
- **Drag and Drop**: Intuitive manipulation of items and world objects
- **Visual Feedback**: Clear indication of interactive elements and actions

## 🔗 Related Repositories

This client is part of the complete Glitch open-source ecosystem:

- **[glitch-GameServerJS](https://github.com/ap0ught/glitch-GameServerJS)** - The complete server-side game logic
- **[glitch-web](https://github.com/tinyspeck/glitch-web)** - Web site and supporting services  
- **[glitch-assets](https://github.com/tinyspeck/glitch-assets)** - Game art, sounds, and animation assets

## 📚 Additional Documentation

- **[DEVELOPMENT.md](DEVELOPMENT.md)** - Developer guide for exploring and understanding the client code
- **[glitch-GameServerJS Architecture](https://github.com/ap0ught/glitch-GameServerJS/blob/main/ARCHITECTURE.md)** - Deep dive into server architecture
- **[glitch-GameServerJS Features](https://github.com/ap0ught/glitch-GameServerJS/blob/main/FEATURES.md)** - Comprehensive breakdown of server-side game systems

## 🎯 Use Cases

### **Educational Applications**
- **Game Development Courses**: Real-world example of MMO client architecture
- **Flash/ActionScript Learning**: Large-scale application patterns and best practices
- **UI/UX Design**: Complex interface design for virtual environments
- **Network Programming**: Client-server communication in real-time applications

### **Research Applications**
- **Virtual Worlds Research**: Avatar systems and digital identity
- **Social Computing**: Online community interfaces and communication
- **Human-Computer Interaction**: Accessibility and usability in virtual spaces
- **Game Studies**: Analysis of successful MMO design patterns

### **Development Reference**
- **Client Architecture**: Patterns for real-time multiplayer game clients
- **Asset Management**: Dynamic loading and caching strategies
- **UI Frameworks**: Component-based interface development
- **Performance Optimization**: Memory and rendering optimization techniques

## 📄 License

All files are provided by Tiny Speck under the [Creative Commons CC0 1.0 Universal License](http://creativecommons.org/publicdomain/zero/1.0/legalcode). This is a broadly permissive "No Rights Reserved" license — you may do what you please with what we've provided.

**Important Notes:**
- All files are provided AS-IS without support
- The Glitch logo and trademark are NOT included in this license
- Only items explicitly included in these files are covered
- No obligation to credit, but links to [glitchthegame.com](http://glitchthegame.com) are appreciated

## 🤝 Contributing

Documentation contributions are welcome! If you figure something out that others could learn from:

1. Write up a clear explanation or how-to guide
2. Submit it as a pull request  
3. Share your knowledge with the community

**Areas where contributions would be valuable:**
- Flash/ActionScript development setup guides
- Code exploration and navigation guides
- Detailed explanations of specific client systems
- Discovery of hidden features or development tools

## ⚖️ Third-Party Components

This repository includes several third-party projects with their own licensing terms:

- **Draw** by Martin Heidegger (`at/leichtgewicht`)
- **Tweener** by Zeh Fernando, Nate Chatellier, Arthur Debert and Francis Turmel (`caurina/transitions`)
- **Adobe Libraries** - Image Encoding, JSON, Base64 (`com/adobe`)
- **Bit101** by Keith Peters (`com/bit101`)
- **GreenSock** animation libraries (`com/greensock`)
- **Quasimondo** EdgeFinder and ColorMatrix (`com/quasimondo`)
- **Bitmap Snapshot** by Stephen Braitsch (`com/quietless`)
- **Object Pool** by Michael Baczynski (`de/polygonal`)
- **Stats** by Mr.doob (`net/hires`)
- **GIF Utilities** by Thibault Imbert (`org/bytearray`)
- **SWF Tools** by Paul Sivtsov (`org/igorcosta`)
- **Fonts and Audio** - Various licensed content in `TSEngineAssets`

*Note: Some proprietary fonts (Helvetica, VAG Rounded) have been removed due to licensing restrictions.*

---

*This client represents the culmination of years of innovative game development, showcasing advanced Flash/ActionScript techniques and MMO client architecture. Whether you're studying game development, researching virtual worlds, or just curious about how Glitch worked, this codebase offers deep insights into creating engaging online experiences.*
