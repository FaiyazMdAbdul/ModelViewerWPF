# 3D Model Viewer & Inspector

## Software Requirements Specification (SRS)

**Document Version:** 1.0
**Status:** Draft
**Author:** Faiyaz M A
**Created:** 2026-02-02
**Last Updated:** 2026-02-02

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Project Overview](#2-project-overview)
3. [Stakeholders](#3-stakeholders)
4. [Functional Requirements](#4-functional-requirements)
5. [Non-Functional Requirements](#5-non-functional-requirements)
6. [System Architecture](#6-system-architecture)
7. [User Interface Specifications](#7-user-interface-specifications)
8. [Data Models](#8-data-models)
9. [File Format Specifications](#9-file-format-specifications)
10. [Integration Points](#10-integration-points)
11. [Security Considerations](#11-security-considerations)
12. [Performance Requirements](#12-performance-requirements)
13. [Testing Strategy](#13-testing-strategy)
14. [Deployment Strategy](#14-deployment-strategy)
15. [Maintenance & Support](#15-maintenance--support)
16. [Risk Assessment](#16-risk-assessment)
17. [Glossary](#17-glossary)
18. [Appendices](#18-appendices)

---

## 1. Executive Summary

### 1.1 Purpose

This document defines the complete software requirements specification for the **3D Model Viewer & Inspector** application. The application provides professional-grade 3D model visualization, inspection, and analysis capabilities for game developers, 3D artists, and technical artists transitioning from Unity XR development to WPF desktop applications.

### 1.2 Scope

The 3D Model Viewer & Inspector is a standalone Windows desktop application built on WPF (.NET 8.0) that enables users to load, view, analyze, and export metadata for 3D model files. The application supports industry-standard file formats and provides comprehensive mesh analysis tools comparable to professional 3D software suites.

### 1.3 Business Objectives

- Provide a lightweight, fast alternative to full 3D suites for quick model inspection
- Enable batch processing of model files for asset pipeline validation
- Serve as a learning platform for WPF 3D graphics programming
- Create a foundation for future asset management tools

### 1.4 Success Criteria

| Metric | Target |
|--------|--------|
| Model load time (< 100k triangles) | < 2 seconds |
| Frame rate during interaction | ≥ 60 FPS |
| Memory usage (idle) | < 200 MB |
| Supported file formats | ≥ 5 formats |
| User satisfaction score | ≥ 4.0/5.0 |

---

## 2. Project Overview

### 2.1 Product Vision

A professional desktop application that combines the simplicity of a file viewer with the analytical depth of professional 3D software, specifically tailored for game development workflows.

### 2.2 Target Audience

| User Type | Description | Primary Use Cases |
|-----------|-------------|-------------------|
| Game Developers | Unity/Unreal developers reviewing assets | Quick model preview, polygon count verification |
| 3D Artists | Modelers and texture artists | Visual QA, UV inspection, material review |
| Technical Artists | Pipeline engineers and tool developers | Batch validation, format conversion verification |
| Project Managers | Non-technical stakeholders | Asset review, approval workflows |

### 2.3 Key Features Summary

1. **Multi-format 3D Model Loading** — Support for OBJ, FBX, STL, GLTF/GLB, DAE
2. **Interactive 3D Viewport** — Orbit, pan, zoom with mouse/keyboard controls
3. **Mesh Analysis Tools** — Vertex count, face count, bounds, topology analysis
4. **Material Inspector** — View and analyze material properties and textures
5. **UV Visualization** — 2D UV layout viewer with overlap detection
6. **Batch Processing** — Process multiple files for report generation
7. **Export Capabilities** — Screenshots, mesh reports, metadata JSON

---

## 3. Stakeholders

### 3.1 Stakeholder Register

| Stakeholder | Role | Interest | Influence |
|-------------|------|----------|-----------|
| Primary Developer | Implementation | High | High |
| End Users (Game Devs) | Consumers | High | Medium |
| QA Testers | Quality Assurance | Medium | Medium |
| Future Maintainers | Long-term support | Medium | Low |

### 3.2 Communication Plan

| Deliverable | Frequency | Format | Audience |
|-------------|-----------|--------|----------|
| Progress Updates | Weekly | Progress Tracker | All |
| Technical Documentation | Per milestone | Markdown | Developers |
| Release Notes | Per release | Changelog | All |

---

## 4. Functional Requirements

### 4.1 File Operations

#### FR-FILE-001: Open Single File
**Priority:** P0 (Critical)
**Description:** User shall be able to open a single 3D model file via file dialog or drag-and-drop.

**Acceptance Criteria:**
- File dialog filters by supported extensions
- Drag-and-drop accepts files onto viewport or window
- Invalid files display descriptive error message
- Loading progress indicator for files > 1 MB
- Recent files list maintained (last 20 files)

#### FR-FILE-002: Open Multiple Files
**Priority:** P1 (High)
**Description:** User shall be able to open multiple files simultaneously for comparison or batch analysis.

**Acceptance Criteria:**
- Multi-select in file dialog
- Tab-based interface for multiple open models
- Maximum of 10 simultaneous models (configurable)
- Memory warning when approaching system limits

#### FR-FILE-003: Drag-and-Drop Support
**Priority:** P1 (High)
**Description:** Application shall accept files via drag-and-drop gesture.

**Acceptance Criteria:**
- Visual feedback when dragging over valid drop zone
- Support for single and multiple file drops
- Support for folder drops (enumerates contents)
- Rejection feedback for unsupported file types

#### FR-FILE-004: Recent Files
**Priority:** P2 (Medium)
**Description:** Application shall maintain a list of recently opened files.

**Acceptance Criteria:**
- Persisted between application sessions
- Maximum 20 entries (configurable)
- Invalid/missing files marked or removed
- Clear history option available
- Pinned files support

#### FR-FILE-005: File Watching
**Priority:** P2 (Medium)
**Description:** Application shall detect external changes to loaded files and offer reload.

**Acceptance Criteria:**
- FileSystemWatcher on loaded file paths
- Non-intrusive notification of changes
- One-click reload option
- Auto-reload toggle (default: off)

---

### 4.2 3D Viewport

#### FR-VIEW-001: Model Rendering
**Priority:** P0 (Critical)
**Description:** Application shall render loaded 3D models with accurate geometry and materials.

**Acceptance Criteria:**
- Triangulated mesh rendering
- Smooth and flat shading modes
- Backface culling toggle
- Wireframe overlay option
- Vertex colors display (if present)

#### FR-VIEW-002: Camera Controls - Orbit
**Priority:** P0 (Critical)
**Description:** User shall orbit the camera around the model using mouse input.

**Acceptance Criteria:**
- Left-click + drag for orbit
- Orbit pivot at model center (default)
- Orbit pivot at clicked point (Shift modifier)
- Configurable orbit sensitivity
- Invert Y-axis option

#### FR-VIEW-003: Camera Controls - Pan
**Priority:** P0 (Critical)
**Description:** User shall pan the camera parallel to the view plane.

**Acceptance Criteria:**
- Middle-click + drag for pan
- Right-click + drag alternative (configurable)
- Pan speed scales with zoom level
- Configurable pan sensitivity

#### FR-VIEW-004: Camera Controls - Zoom
**Priority:** P0 (Critical)
**Description:** User shall zoom the camera toward/away from the model.

**Acceptance Criteria:**
- Scroll wheel for zoom
- Zoom toward cursor position
- Minimum and maximum zoom limits
- Smooth zoom animation (optional)
- Zoom-to-fit button (F key)

#### FR-VIEW-005: Camera Presets
**Priority:** P1 (High)
**Description:** User shall access preset camera angles via keyboard shortcuts or buttons.

**Acceptance Criteria:**
- Front (Numpad 1), Back (Ctrl+Numpad 1)
- Right (Numpad 3), Left (Ctrl+Numpad 3)
- Top (Numpad 7), Bottom (Ctrl+Numpad 7)
- Perspective/Orthographic toggle (Numpad 5)
- Animated transitions between views

#### FR-VIEW-006: Grid and Axes
**Priority:** P1 (High)
**Description:** Application shall display reference grid and coordinate axes.

**Acceptance Criteria:**
- Infinite ground plane grid
- Grid scale adapts to model size
- RGB axis indicator (X=Red, Y=Green, Z=Blue)
- Toggle visibility for grid and axes independently
- Grid snapping options

#### FR-VIEW-007: Environment Lighting
**Priority:** P1 (High)
**Description:** Application shall provide configurable lighting environments.

**Acceptance Criteria:**
- Default three-point lighting setup
- HDRI environment maps support
- Ambient light intensity control
- Shadow casting toggle
- Multiple preset lighting rigs

#### FR-VIEW-008: Render Modes
**Priority:** P1 (High)
**Description:** User shall switch between different visualization modes.

**Acceptance Criteria:**
- Solid (default)
- Wireframe
- Solid + Wireframe overlay
- Vertex colors
- UV checker pattern
- Normal vectors display
- Matcap shading

#### FR-VIEW-009: Selection
**Priority:** P2 (Medium)
**Description:** User shall select mesh components for detailed inspection.

**Acceptance Criteria:**
- Click to select mesh/submesh
- Highlight selected elements
- Selection info displayed in Inspector panel
- Multi-select with Ctrl modifier
- Select all (Ctrl+A), Deselect (Escape)

#### FR-VIEW-010: Measurement Tools
**Priority:** P2 (Medium)
**Description:** User shall measure distances and angles in the viewport.

**Acceptance Criteria:**
- Point-to-point distance measurement
- Angle measurement between faces
- Bounding box dimensions display
- Unit system toggle (metric/imperial/Unity units)
- Persistent measurements until cleared

---

### 4.3 Mesh Analysis

#### FR-MESH-001: Basic Statistics
**Priority:** P0 (Critical)
**Description:** Application shall display fundamental mesh statistics.

**Acceptance Criteria:**
- Vertex count
- Triangle/Face count
- Edge count
- Submesh/Object count
- Bounding box dimensions
- Model center point

#### FR-MESH-002: Topology Analysis
**Priority:** P1 (High)
**Description:** Application shall analyze mesh topology and report issues.

**Acceptance Criteria:**
- Non-manifold edge detection
- Open edge (boundary) detection
- Isolated vertex detection
- Degenerate face detection (zero-area triangles)
- T-vertex detection
- Visual highlighting of problematic areas

#### FR-MESH-003: Normal Analysis
**Priority:** P1 (High)
**Description:** Application shall analyze and visualize vertex/face normals.

**Acceptance Criteria:**
- Normal vector visualization
- Flipped normal detection
- Hard/soft edge visualization
- Normal consistency check
- Average normal direction display

#### FR-MESH-004: UV Analysis
**Priority:** P1 (High)
**Description:** Application shall analyze UV mapping quality.

**Acceptance Criteria:**
- UV coverage percentage
- UV overlap detection and visualization
- UV stretching/distortion heatmap
- UV island count
- Out-of-bounds UV detection
- Texel density visualization

#### FR-MESH-005: Level of Detail (LOD) Analysis
**Priority:** P2 (Medium)
**Description:** Application shall provide LOD-related analysis for game assets.

**Acceptance Criteria:**
- Silhouette edge analysis
- Polycount recommendations per platform
- Screen-size to polycount ratio calculator
- LOD comparison view (if multiple LODs loaded)

#### FR-MESH-006: Batch Analysis
**Priority:** P2 (Medium)
**Description:** Application shall analyze multiple models and generate aggregate reports.

**Acceptance Criteria:**
- Folder selection for batch input
- Progress indication for batch processing
- CSV/JSON export of analysis results
- Summary statistics (min, max, average, total)
- Filter and sort results

---

### 4.4 Material Inspection

#### FR-MAT-001: Material List
**Priority:** P1 (High)
**Description:** Application shall list all materials used in the model.

**Acceptance Criteria:**
- Material name and index
- Face count per material
- Color preview swatch
- Click to isolate material in viewport

#### FR-MAT-002: Material Properties
**Priority:** P1 (High)
**Description:** Application shall display detailed material properties.

**Acceptance Criteria:**
- Diffuse/Albedo color
- Specular/Metallic value
- Roughness/Smoothness value
- Emission properties
- Opacity/Transparency settings
- Shader type (if available)

#### FR-MAT-003: Texture References
**Priority:** P1 (High)
**Description:** Application shall display and preview referenced textures.

**Acceptance Criteria:**
- Texture file paths (absolute and relative)
- Texture resolution display
- Texture format (PNG, JPG, TGA, etc.)
- Thumbnail preview
- Missing texture indication
- Click to open in system viewer

#### FR-MAT-004: Texture Slots
**Priority:** P1 (High)
**Description:** Application shall identify and display texture slot assignments.

**Acceptance Criteria:**
- Diffuse/Albedo map
- Normal map
- Metallic/Roughness map
- Ambient Occlusion map
- Emission map
- Custom/Unknown slots

---

### 4.5 Export Functions

#### FR-EXP-001: Screenshot Export
**Priority:** P1 (High)
**Description:** User shall export viewport as image file.

**Acceptance Criteria:**
- PNG and JPG format support
- Configurable resolution (1x, 2x, 4x, custom)
- Transparent background option
- Include/exclude UI elements
- Batch screenshot for camera presets

#### FR-EXP-002: Report Export
**Priority:** P1 (High)
**Description:** User shall export mesh analysis as document.

**Acceptance Criteria:**
- JSON format for programmatic use
- CSV format for spreadsheet analysis
- HTML format for human-readable reports
- PDF export for formal documentation
- Customizable report templates

#### FR-EXP-003: Metadata Export
**Priority:** P2 (Medium)
**Description:** User shall export model metadata in standard formats.

**Acceptance Criteria:**
- Unity-compatible asset metadata
- Unreal-compatible asset metadata
- Custom JSON schema support
- Batch metadata export

---

### 4.6 User Interface

#### FR-UI-001: Main Window Layout
**Priority:** P0 (Critical)
**Description:** Application shall provide professional multi-panel layout.

**Acceptance Criteria:**
- Resizable panel system
- Panel docking and undocking
- Layout save/restore
- Default layout presets
- Fullscreen viewport mode (F11)

#### FR-UI-002: Menu System
**Priority:** P0 (Critical)
**Description:** Application shall provide comprehensive menu system.

**Acceptance Criteria:**
- File menu (Open, Recent, Close, Exit)
- Edit menu (Preferences, Keyboard shortcuts)
- View menu (Panels, Render modes, Camera)
- Tools menu (Analysis, Measurements)
- Help menu (Documentation, About)
- Keyboard shortcuts for all major functions

#### FR-UI-003: Toolbar
**Priority:** P1 (High)
**Description:** Application shall provide quick-access toolbar.

**Acceptance Criteria:**
- Customizable toolbar
- Icon + text / Icon only / Text only modes
- Tool grouping
- Overflow handling for small windows

#### FR-UI-004: Status Bar
**Priority:** P1 (High)
**Description:** Application shall display contextual status information.

**Acceptance Criteria:**
- Current file name and path
- Polygon/vertex count
- Viewport FPS
- Memory usage
- Mouse position in 3D space
- Zoom level

#### FR-UI-005: Keyboard Shortcuts
**Priority:** P1 (High)
**Description:** Application shall support comprehensive keyboard shortcuts.

**Acceptance Criteria:**
- Industry-standard defaults (similar to Maya/Blender)
- Fully customizable bindings
- Shortcut conflict detection
- Import/export shortcut schemes
- Cheat sheet view (Ctrl+/)

#### FR-UI-006: Theming
**Priority:** P2 (Medium)
**Description:** Application shall support visual themes.

**Acceptance Criteria:**
- Light theme
- Dark theme (default)
- High contrast theme
- Custom theme support
- Per-element color customization

#### FR-UI-007: Preferences Dialog
**Priority:** P1 (High)
**Description:** Application shall provide comprehensive settings management.

**Acceptance Criteria:**
- Categorized settings pages
- Search within preferences
- Reset to defaults (per category and global)
- Import/export preferences
- Changes apply immediately with undo option

---

## 5. Non-Functional Requirements

### 5.1 Performance

| Requirement ID | Description | Target | Priority |
|----------------|-------------|--------|----------|
| NFR-PERF-001 | Application startup time | < 3 seconds | P0 |
| NFR-PERF-002 | Model load time (100k tris) | < 2 seconds | P0 |
| NFR-PERF-003 | Model load time (1M tris) | < 10 seconds | P1 |
| NFR-PERF-004 | Viewport frame rate | ≥ 60 FPS | P0 |
| NFR-PERF-005 | UI responsiveness | < 100ms input latency | P0 |
| NFR-PERF-006 | Memory usage (idle) | < 200 MB | P1 |
| NFR-PERF-007 | Memory usage (1M tri model) | < 1 GB | P1 |

### 5.2 Reliability

| Requirement ID | Description | Target | Priority |
|----------------|-------------|--------|----------|
| NFR-REL-001 | Crash rate | < 0.1% of sessions | P0 |
| NFR-REL-002 | Data corruption rate | 0% | P0 |
| NFR-REL-003 | Recovery from invalid files | 100% graceful handling | P0 |
| NFR-REL-004 | Session recovery | Auto-save state every 5 min | P2 |

### 5.3 Usability

| Requirement ID | Description | Target | Priority |
|----------------|-------------|--------|----------|
| NFR-USE-001 | Time to first successful load | < 30 seconds for new user | P1 |
| NFR-USE-002 | Feature discoverability | Tooltips on all buttons | P1 |
| NFR-USE-003 | Error message clarity | Actionable error messages | P0 |
| NFR-USE-004 | Accessibility | WCAG 2.1 AA compliance | P2 |

### 5.4 Maintainability

| Requirement ID | Description | Target | Priority |
|----------------|-------------|--------|----------|
| NFR-MNT-001 | Code coverage | ≥ 80% | P1 |
| NFR-MNT-002 | Documentation | All public APIs documented | P1 |
| NFR-MNT-003 | Cyclomatic complexity | ≤ 10 per method | P2 |
| NFR-MNT-004 | Technical debt ratio | < 5% | P2 |

### 5.5 Portability

| Requirement ID | Description | Target | Priority |
|----------------|-------------|--------|----------|
| NFR-PORT-001 | Windows version support | Windows 10 21H2+, Windows 11 | P0 |
| NFR-PORT-002 | .NET version | .NET 8.0 LTS | P0 |
| NFR-PORT-003 | DPI scaling | 100%, 125%, 150%, 200% | P1 |
| NFR-PORT-004 | Multi-monitor support | Proper window management | P1 |

---

## 6. System Architecture

### 6.1 High-Level Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        Presentation Layer                        │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────────┐  │
│  │   Views     │  │  ViewModels │  │  Converters/Behaviors   │  │
│  │   (XAML)    │  │   (C#)      │  │                         │  │
│  └─────────────┘  └─────────────┘  └─────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                        Application Layer                         │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────────┐  │
│  │  Commands   │  │  Services   │  │     Event Aggregator    │  │
│  │             │  │             │  │                         │  │
│  └─────────────┘  └─────────────┘  └─────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                         Domain Layer                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────────┐  │
│  │   Models    │  │  Analysis   │  │     Validation          │  │
│  │             │  │   Engine    │  │                         │  │
│  └─────────────┘  └─────────────┘  └─────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                      Infrastructure Layer                        │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────────┐  │
│  │File Parsers │  │  Rendering  │  │   Persistence/Config    │  │
│  │(OBJ,FBX...) │  │  (Helix3D)  │  │                         │  │
│  └─────────────┘  └─────────────┘  └─────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
```

### 6.2 Project Structure

```
ModelViewer/
├── src/
│   ├── ModelViewer.App/                 # Main application (entry point)
│   │   ├── App.xaml(.cs)
│   │   ├── MainWindow.xaml(.cs)
│   │   └── Startup/
│   │       ├── Bootstrapper.cs
│   │       └── ServiceRegistration.cs
│   │
│   ├── ModelViewer.Core/                # Domain models and interfaces
│   │   ├── Models/
│   │   │   ├── Scene.cs
│   │   │   ├── MeshData.cs
│   │   │   ├── MaterialData.cs
│   │   │   ├── TextureReference.cs
│   │   │   └── AnalysisResult.cs
│   │   ├── Interfaces/
│   │   │   ├── IModelLoader.cs
│   │   │   ├── IAnalysisEngine.cs
│   │   │   └── IExportService.cs
│   │   └── Enums/
│   │       ├── RenderMode.cs
│   │       └── AnalysisType.cs
│   │
│   ├── ModelViewer.Analysis/            # Mesh analysis algorithms
│   │   ├── TopologyAnalyzer.cs
│   │   ├── UVAnalyzer.cs
│   │   ├── NormalAnalyzer.cs
│   │   └── StatisticsCalculator.cs
│   │
│   ├── ModelViewer.Infrastructure/      # External integrations
│   │   ├── FileLoaders/
│   │   │   ├── ObjLoader.cs
│   │   │   ├── FbxLoader.cs
│   │   │   ├── GltfLoader.cs
│   │   │   └── StlLoader.cs
│   │   ├── Rendering/
│   │   │   ├── HelixViewportAdapter.cs
│   │   │   └── ShaderManager.cs
│   │   └── Persistence/
│   │       ├── SettingsService.cs
│   │       └── RecentFilesService.cs
│   │
│   ├── ModelViewer.UI/                  # Presentation layer
│   │   ├── Views/
│   │   │   ├── ViewportView.xaml
│   │   │   ├── InspectorView.xaml
│   │   │   ├── HierarchyView.xaml
│   │   │   └── MaterialsView.xaml
│   │   ├── ViewModels/
│   │   │   ├── MainViewModel.cs
│   │   │   ├── ViewportViewModel.cs
│   │   │   ├── InspectorViewModel.cs
│   │   │   └── MaterialsViewModel.cs
│   │   ├── Controls/
│   │   │   ├── PropertyGrid.xaml
│   │   │   └── ColorPicker.xaml
│   │   ├── Converters/
│   │   └── Behaviors/
│   │
│   └── ModelViewer.Export/              # Export functionality
│       ├── ScreenshotExporter.cs
│       ├── ReportGenerator.cs
│       └── Templates/
│
├── tests/
│   ├── ModelViewer.Core.Tests/
│   ├── ModelViewer.Analysis.Tests/
│   ├── ModelViewer.Infrastructure.Tests/
│   └── ModelViewer.UI.Tests/
│
├── docs/
│   ├── api/
│   ├── user-guide/
│   └── architecture/
│
├── assets/
│   ├── icons/
│   ├── themes/
│   └── sample-models/
│
├── ModelViewer.sln
├── README.md
├── scope.md
├── progress.md
└── CHANGELOG.md
```

### 6.3 Technology Stack

| Layer | Technology | Version | Justification |
|-------|------------|---------|---------------|
| Framework | .NET | 8.0 LTS | Long-term support, performance |
| UI Framework | WPF | Built-in | Rich desktop UI, XAML data binding |
| 3D Rendering | HelixToolkit.WPF | 2.x | Mature WPF 3D library |
| MVVM Framework | CommunityToolkit.Mvvm | 8.x | Microsoft-backed, source generators |
| Dependency Injection | Microsoft.Extensions.DI | 8.x | Standard .NET DI container |
| Logging | Serilog | 3.x | Structured logging, multiple sinks |
| Settings | System.Text.Json | Built-in | Fast, native JSON support |
| FBX Parsing | Assimp.NET | 5.x | Comprehensive format support |
| Testing | xUnit + Moq | Latest | Industry standard |
| UI Testing | Appium WinAppDriver | Latest | Windows UI automation |

### 6.4 Design Patterns

| Pattern | Usage |
|---------|-------|
| MVVM | Separation of UI and business logic |
| Repository | Abstraction over file system operations |
| Strategy | Interchangeable file loaders |
| Observer | Event-based communication between components |
| Command | Encapsulated user actions with undo/redo |
| Factory | Creation of model loaders and analyzers |
| Singleton | Application-wide services (settings, logging) |

---

## 7. User Interface Specifications

### 7.1 Main Window Wireframe

```
┌─────────────────────────────────────────────────────────────────────────┐
│ File   Edit   View   Tools   Help                              _ □ X   │
├─────────────────────────────────────────────────────────────────────────┤
│ [Open] [Save] [|] [Solid▼] [Wireframe] [|] [Grid] [Axes] [|] [Measure] │
├───────────────┬─────────────────────────────────────────┬───────────────┤
│   HIERARCHY   │                                         │   INSPECTOR   │
│ ─────────────│                                         │ ─────────────│
│ ▼ Scene       │                                         │ Statistics    │
│   ▼ Model     │                                         │ ───────────── │
│     └ Mesh001 │          3D VIEWPORT                    │ Vertices: 1.2k│
│     └ Mesh002 │                                         │ Triangles: 2k │
│     └ Mesh003 │              [Model]                    │ Materials: 3  │
│               │                                         │               │
│               │                                         │ Bounds        │
│               │           ──────────                    │ ───────────── │
│               │           Grid Floor                    │ X: 1.5m       │
│               │                                         │ Y: 2.0m       │
│               │                                         │ Z: 1.2m       │
│               │                                         │               │
│               │                                         │ Analysis      │
│               │                                         │ ───────────── │
│               │                                         │ [Run Analysis]│
├───────────────┴─────────────────────────────────────────┴───────────────┤
│   MATERIALS                    │           UV VIEWER                    │
│ ───────────────────────────────│─────────────────────────────────────── │
│ [■] Material_01  (500 faces)  │                                        │
│ [■] Material_02  (800 faces)  │     UV Layout Preview                  │
│ [■] Material_03  (700 faces)  │                                        │
├─────────────────────────────────────────────────────────────────────────┤
│ Model.fbx │ 2,000 tris │ 1,234 verts │ 60 FPS │ 156 MB      │ Ready    │
└─────────────────────────────────────────────────────────────────────────┘
```

### 7.2 Panel Specifications

#### 7.2.1 Hierarchy Panel
- **Purpose:** Display scene graph and object hierarchy
- **Width:** 200px (default), resizable 150-400px
- **Features:**
  - Tree view with expand/collapse
  - Icons for object types (mesh, empty, camera, light)
  - Right-click context menu
  - Drag to reorder (future)
  - Search/filter box

#### 7.2.2 Inspector Panel
- **Purpose:** Display properties of selected object
- **Width:** 280px (default), resizable 200-500px
- **Sections:**
  - Transform (position, rotation, scale)
  - Mesh Statistics
  - Bounding Box
  - Analysis Results
  - Material Assignments

#### 7.2.3 Viewport
- **Purpose:** 3D model visualization
- **Background:** Gradient (configurable)
- **Overlays:**
  - FPS counter (toggle)
  - Axis indicator (corner)
  - Selection info
  - Measurement displays

#### 7.2.4 Materials Panel
- **Purpose:** List and inspect materials
- **Height:** 150px (default), collapsible
- **Features:**
  - Material swatches
  - Face count per material
  - Click to select/isolate
  - Texture path display

#### 7.2.5 UV Viewer Panel
- **Purpose:** 2D UV layout visualization
- **Height:** 150px (default), collapsible
- **Features:**
  - UV island display
  - Overlap highlighting
  - Zoom and pan
  - Checker pattern toggle

### 7.3 Color Scheme (Dark Theme)

| Element | Color | Hex |
|---------|-------|-----|
| Background (Primary) | Dark Gray | #1E1E1E |
| Background (Secondary) | Darker Gray | #252526 |
| Background (Tertiary) | Medium Gray | #333333 |
| Text (Primary) | White | #FFFFFF |
| Text (Secondary) | Light Gray | #CCCCCC |
| Text (Disabled) | Gray | #666666 |
| Accent (Primary) | Blue | #0078D4 |
| Accent (Hover) | Light Blue | #1084D8 |
| Success | Green | #4EC9B0 |
| Warning | Yellow | #DCDCAA |
| Error | Red | #F14C4C |
| Border | Dark Border | #3F3F46 |

---

## 8. Data Models

### 8.1 Core Domain Models

```csharp
public class Scene
{
    public string FilePath { get; set; }
    public string FileName { get; set; }
    public DateTime LoadedAt { get; set; }
    public List<SceneObject> RootObjects { get; set; }
    public List<MaterialData> Materials { get; set; }
    public List<TextureReference> Textures { get; set; }
    public SceneStatistics Statistics { get; set; }
}

public class SceneObject
{
    public string Name { get; set; }
    public Guid Id { get; set; }
    public Matrix3D Transform { get; set; }
    public MeshData Mesh { get; set; }
    public int MaterialIndex { get; set; }
    public List<SceneObject> Children { get; set; }
}

public class MeshData
{
    public Vector3D[] Vertices { get; set; }
    public int[] Indices { get; set; }
    public Vector3D[] Normals { get; set; }
    public Vector2D[] UVs { get; set; }
    public Color[] VertexColors { get; set; }
    public BoundingBox Bounds { get; set; }
}

public class MaterialData
{
    public string Name { get; set; }
    public Color DiffuseColor { get; set; }
    public Color SpecularColor { get; set; }
    public float Metallic { get; set; }
    public float Roughness { get; set; }
    public float Opacity { get; set; }
    public Dictionary<TextureSlot, TextureReference> Textures { get; set; }
}

public class TextureReference
{
    public string FilePath { get; set; }
    public string ResolvedPath { get; set; }
    public bool Exists { get; set; }
    public int Width { get; set; }
    public int Height { get; set; }
    public string Format { get; set; }
}

public class AnalysisResult
{
    public AnalysisType Type { get; set; }
    public AnalysisSeverity Severity { get; set; }
    public string Message { get; set; }
    public List<int> AffectedElements { get; set; }
    public Dictionary<string, object> Data { get; set; }
}

public class SceneStatistics
{
    public int TotalVertices { get; set; }
    public int TotalTriangles { get; set; }
    public int TotalEdges { get; set; }
    public int ObjectCount { get; set; }
    public int MaterialCount { get; set; }
    public int TextureCount { get; set; }
    public BoundingBox SceneBounds { get; set; }
    public long FileSizeBytes { get; set; }
    public TimeSpan LoadTime { get; set; }
}
```

### 8.2 Settings Model

```csharp
public class ApplicationSettings
{
    public ViewportSettings Viewport { get; set; }
    public UISettings UI { get; set; }
    public PerformanceSettings Performance { get; set; }
    public KeyboardShortcuts Shortcuts { get; set; }
}

public class ViewportSettings
{
    public Color BackgroundColor { get; set; }
    public bool ShowGrid { get; set; }
    public bool ShowAxes { get; set; }
    public float GridSize { get; set; }
    public RenderMode DefaultRenderMode { get; set; }
    public CameraSettings Camera { get; set; }
}

public class CameraSettings
{
    public float OrbitSensitivity { get; set; }
    public float PanSensitivity { get; set; }
    public float ZoomSensitivity { get; set; }
    public bool InvertY { get; set; }
    public bool SmoothCamera { get; set; }
}
```

---

## 9. File Format Specifications

### 9.1 Supported Import Formats

| Format | Extension | Priority | Parser | Notes |
|--------|-----------|----------|--------|-------|
| Wavefront OBJ | .obj | P0 | Custom | With MTL support |
| FBX | .fbx | P0 | Assimp | Binary and ASCII |
| glTF | .gltf, .glb | P1 | Assimp | 2.0 spec |
| STL | .stl | P1 | Custom | Binary and ASCII |
| COLLADA | .dae | P2 | Assimp | 1.4 and 1.5 |
| 3DS | .3ds | P3 | Assimp | Legacy support |
| PLY | .ply | P3 | Assimp | Point cloud support |

### 9.2 Export Formats

| Format | Extension | Use Case |
|--------|-----------|----------|
| PNG | .png | Screenshots with transparency |
| JPEG | .jpg | Screenshots optimized for size |
| JSON | .json | Analysis data, metadata |
| CSV | .csv | Spreadsheet-compatible reports |
| HTML | .html | Human-readable reports |
| PDF | .pdf | Formal documentation |

---

## 10. Integration Points

### 10.1 External Tool Integration

| Integration | Method | Purpose |
|-------------|--------|---------|
| Windows Explorer | Shell extension | "Open with" context menu |
| Unity | Custom protocol | Open models directly from Unity |
| Blender | Script output | Import analysis reports |
| Version Control | File watching | Auto-reload on external change |

### 10.2 API Extensibility

The application shall expose a plugin API for:
- Custom file format loaders
- Custom analysis modules
- Custom export formats
- UI extensions (panels, tools)

```csharp
public interface IModelLoaderPlugin
{
    string Name { get; }
    string[] SupportedExtensions { get; }
    Scene Load(string filePath, LoadOptions options);
}

public interface IAnalysisPlugin
{
    string Name { get; }
    string Category { get; }
    AnalysisResult[] Analyze(MeshData mesh, AnalysisOptions options);
}
```

---

## 11. Security Considerations

### 11.1 File Handling

| Risk | Mitigation |
|------|------------|
| Malformed file causing crash | Sandboxed parsing with exception handling |
| Path traversal in file references | Sanitize and validate all paths |
| Memory exhaustion from large files | File size limits, streaming for large files |
| Malicious scripts in FBX | Disable script execution in Assimp |

### 11.2 Data Protection

| Risk | Mitigation |
|------|------------|
| Sensitive file paths in recent files | Optional path obfuscation |
| Settings file tampering | Validation on load, graceful fallback |
| Crash dump data exposure | Exclude sensitive data from logs |

---

## 12. Performance Requirements

### 12.1 Benchmarks

| Scenario | Model Size | Target Load Time | Target FPS |
|----------|------------|------------------|------------|
| Simple | < 10k tris | < 0.5s | 60 FPS |
| Standard | 10k-100k tris | < 2s | 60 FPS |
| Complex | 100k-500k tris | < 5s | 30+ FPS |
| Heavy | 500k-1M tris | < 10s | 30+ FPS |
| Extreme | > 1M tris | < 30s | 15+ FPS |

### 12.2 Optimization Strategies

1. **Level of Detail (LOD) Generation** — Auto-generate simplified meshes for viewport
2. **Frustum Culling** — Don't render off-screen geometry
3. **Occlusion Culling** — Skip hidden geometry (for complex scenes)
4. **Progressive Loading** — Display partial model while loading
5. **Background Threading** — Parse files off UI thread
6. **Memory Pooling** — Reuse buffers for mesh data
7. **Lazy Texture Loading** — Load textures on demand

---

## 13. Testing Strategy

### 13.1 Test Categories

| Category | Coverage Target | Tools |
|----------|-----------------|-------|
| Unit Tests | 80% | xUnit, Moq |
| Integration Tests | 60% | xUnit, TestContainers |
| UI Tests | 40% | WinAppDriver, Appium |
| Performance Tests | Key paths | BenchmarkDotNet |
| Manual Tests | Edge cases | Test scripts |

### 13.2 Test Scenarios

#### 13.2.1 File Loading Tests
- Load valid OBJ file
- Load valid FBX file (ASCII and binary)
- Load file with missing textures
- Load file with invalid geometry
- Load file with special characters in path
- Load extremely large file (memory handling)
- Load empty file
- Load corrupted file

#### 13.2.2 Viewport Tests
- Orbit camera 360 degrees
- Pan camera in all directions
- Zoom in/out full range
- Switch between render modes
- Toggle grid and axes
- Frame selection
- Handle window resize
- Handle DPI change

#### 13.2.3 Analysis Tests
- Verify vertex count accuracy
- Verify triangle count accuracy
- Detect non-manifold edges
- Detect UV overlaps
- Detect flipped normals
- Handle meshes without UVs
- Handle meshes without normals

---

## 14. Deployment Strategy

### 14.1 Distribution Methods

| Method | Target Audience | Update Mechanism |
|--------|-----------------|------------------|
| MSIX Package | Windows Store | Auto-update |
| MSI Installer | Enterprise | Manual/SCCM |
| Portable ZIP | Developers | Manual |
| ClickOnce | Quick deploy | Auto-update |

### 14.2 System Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| OS | Windows 10 21H2 | Windows 11 |
| CPU | Dual-core 2.0 GHz | Quad-core 3.0 GHz |
| RAM | 4 GB | 16 GB |
| GPU | DirectX 11 | DirectX 12, 4GB VRAM |
| Storage | 200 MB | 500 MB |
| Display | 1280x720 | 1920x1080 |

---

## 15. Maintenance & Support

### 15.1 Support Tiers

| Tier | Response Time | Scope |
|------|---------------|-------|
| Critical (Crash/Data Loss) | 24 hours | Hotfix release |
| High (Feature Broken) | 1 week | Next patch release |
| Medium (Minor Issue) | 2 weeks | Next minor release |
| Low (Enhancement) | Backlog | Future release |

### 15.2 Logging Strategy

```
Logs/
├── ModelViewer-2026-02-02.log      # Daily rolling file
├── ModelViewer-2026-02-01.log
└── ModelViewer-errors.log           # Errors only (persistent)
```

Log levels: Verbose, Debug, Information, Warning, Error, Fatal

---

## 16. Risk Assessment

### 16.1 Risk Register

| Risk ID | Description | Probability | Impact | Mitigation |
|---------|-------------|-------------|--------|------------|
| R001 | HelixToolkit version conflicts | Medium | High | Pin version, abstract adapter |
| R002 | FBX format changes | Low | Medium | Assimp abstraction layer |
| R003 | Performance issues with large files | High | High | LOD, streaming, limits |
| R004 | Memory leaks in 3D rendering | Medium | High | Dispose patterns, profiling |
| R005 | Cross-DPI rendering issues | Medium | Medium | WPF DPI awareness APIs |
| R006 | Scope creep | High | Medium | Strict scope control |

### 16.2 Contingency Plans

| Risk | Contingency |
|------|-------------|
| HelixToolkit issues | Fallback to SharpDX or MonoGame |
| Performance targets missed | Reduce default quality, add quality presets |
| Memory issues | Implement model size limits with warnings |

---

## 17. Glossary

| Term | Definition |
|------|------------|
| **Mesh** | Collection of vertices, edges, and faces defining 3D geometry |
| **Submesh** | Subset of a mesh, typically with distinct material |
| **UV** | 2D texture coordinates mapped to 3D surface |
| **Normal** | Vector perpendicular to surface, used for lighting |
| **LOD** | Level of Detail - simplified geometry for performance |
| **MVVM** | Model-View-ViewModel architectural pattern |
| **Frustum** | The visible region of 3D space from camera perspective |
| **Matcap** | Material capture - pre-lit material for fast preview |

---

## 18. Appendices

### Appendix A: Keyboard Shortcuts (Default)

| Action | Shortcut |
|--------|----------|
| Open File | Ctrl+O |
| Close File | Ctrl+W |
| Save Screenshot | Ctrl+S |
| Undo | Ctrl+Z |
| Redo | Ctrl+Y |
| Fullscreen | F11 |
| Frame Selection | F |
| Toggle Wireframe | Z |
| Toggle Grid | G |
| Front View | Numpad 1 |
| Right View | Numpad 3 |
| Top View | Numpad 7 |
| Perspective/Ortho | Numpad 5 |
| Reset Camera | Home |
| Show Shortcuts | Ctrl+/ |

### Appendix B: Sample Analysis Report (JSON)

```json
{
  "file": "character_model.fbx",
  "timestamp": "2026-02-02T14:30:00Z",
  "statistics": {
    "vertices": 12450,
    "triangles": 24000,
    "materials": 3,
    "textures": 5
  },
  "bounds": {
    "min": [-0.5, 0.0, -0.3],
    "max": [0.5, 1.8, 0.3],
    "size": [1.0, 1.8, 0.6]
  },
  "issues": [
    {
      "type": "NON_MANIFOLD_EDGE",
      "severity": "WARNING",
      "count": 2,
      "details": "Found at edges [1234, 5678]"
    }
  ]
}
```

### Appendix C: Related Documents

- [Progress Tracker](./progress.md)
- [Architecture Decision Records](./docs/architecture/ADR/)
- [User Guide](./docs/user-guide/)
- [API Reference](./docs/api/)

---

**Document Approval**

| Role | Name | Date | Signature |
|------|------|------|-----------|
| Author | | | |
| Technical Lead | | | |
| Product Owner | | | |
| QA Lead | | | |
