# Roblox Offline Player

Play Roblox games offline by loading `.rbxl` (Roblox Place) files directly into your browser or desktop client. This application parses binary Roblox place files, extracts game data, and executes them in a Roblox-compatible environment.

## Features

- 🎮 **Open .rbxl files** - Load Roblox place files directly
- 🔧 **Compile & Execute** - Converts place data into runnable game code
- 🎯 **Game Fidelity** - Maintains original game logic and structure
- 💻 **Offline Play** - No internet required after loading the file
- 🌐 **Web & Desktop** - Works in browser or as Electron app
- 📦 **Asset Support** - Handles textures, sounds, and models
- ⚙️ **Lua Support** - Executes Lua scripts embedded in places

## Project Structure

```
src/
  server/           Express.js backend for file handling
    index.ts        Entry point
    routes/         API routes for file upload/download
    parser/         RBXL binary parser
    compiler/       Place-to-runtime compiler
  client/           Web frontend (React/TypeScript)
    App.tsx         Main UI component
    components/     UI components (file upload, viewer, player)
    game/           Game runtime and renderer
  shared/           Shared types and utilities
    types.ts        TypeScript interfaces
    constants.ts    Game engine constants
tests/              Test suite
public/             Static assets
```

## Getting Started

### Prerequisites
- Node.js 18+
- npm or yarn

### Installation

```bash
git clone https://github.com/wyatt232/RobloxInBrowserSoAmazing
cd RobloxInBrowserSoAmazing
npm install
```

### Development

```bash
npm run dev
```

This starts the server on `http://localhost:3000` with hot-reload.

### Build for Production

```bash
npm run build
npm start
```

## Usage

1. **Open the Application**
   - Navigate to `http://localhost:3000` in your browser

2. **Load a .rbxl File**
   - Click "Open File" and select your `.rbxl` file
   - The parser will extract the game structure

3. **Play**
   - Click "Run Game" to compile and start playing
   - Use mouse and keyboard controls like normal Roblox

## .rbxl File Format

Roblox place files are binary format containing:
- **Instance hierarchy** - Game objects and their properties
- **Lua scripts** - Game logic and server/client scripts
- **Assets** - Textures, models, sounds, animations
- **Metadata** - Game settings, lighting, physics parameters

The parser extracts this data into a JSON-compatible format for processing.

## Game Engine

The runtime uses a custom game engine that:
- Simulates Roblox's Instance/Object model
- Executes Lua scripts via WebAssembly Lua VM
- Renders 3D scenes using Three.js
- Handles physics via Cannon.js
- Manages networking for multiplayer (future)

## Architecture

### Parser (`src/server/parser/`)
- Binary RBXL file reader
- Instance hierarchy extractor
- Asset catalog builder

### Compiler (`src/server/compiler/`)
- Converts extracted data to runtime format
- Optimizes Lua bytecode
- Pre-loads assets

### Runtime (`src/client/game/`)
- Instance system (matching Roblox API)
- Lua execution engine
- 3D rendering pipeline
- Input handling
- Physics simulation

## Supported Features

- ✅ Instance/Object model
- ✅ Lua scripting (LocalScripts, Scripts)
- ✅ GUI rendering (2D UI)
- ✅ 3D models and meshes
- ✅ Physics (basic)
- ✅ Humanoid controls
- ✅ Events and connections
- 🔄 Networking (in progress)
- 🔄 Advanced physics (in progress)
- 🔄 Particle effects (in progress)

## API Endpoints

### `POST /api/upload`
Upload a `.rbxl` file for parsing.

**Request:**
```
multipart/form-data
- file: binary .rbxl file
```

**Response:**
```json
{
  "id": "unique-session-id",
  "name": "Game Name",
  "data": { /* parsed place data */ }
}
```

### `GET /api/game/:id`
Retrieve parsed game data.

### `POST /api/compile`
Compile game data to runnable format.

## Troubleshooting

- **File won't load** - Ensure it's a valid `.rbxl` file (not `.rbxm` or other formats)
- **Scripts don't run** - Check browser console for Lua errors
- **Performance issues** - Reduce draw distance or disable physics

## Contributing

Contributions welcome! Areas needing work:
- Advanced Lua compatibility
- Network replication
- Physics accuracy
- Performance optimization
- Asset loading edge cases

## License

MIT

## Disclaimer

This project is for educational purposes. Respect Roblox's terms of service and intellectual property. Only load games you have permission to play offline.
