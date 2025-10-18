# Path of Building Font Generator

This utility builds bitmap fonts used by the Path of Building Community fork. It wraps Windows GDI font rendering into a standalone Win32 application that packs glyphs into `.tga` atlases and emits metadata consumed by the main tool.

## Prerequisites
- Visual Studio 2022 (v143 toolset) with the Desktop development with C++ workload
- Windows 10 SDK (10.0 or newer)

## Building
1. Open `GLFontGen.sln` in Visual Studio.
2. Select the desired configuration (`Release` is recommended for distributing fonts).
3. Build the solution (`Build > Build Solution`).

The resulting executable (`GLFontGen.exe`) stays local to your build environment; it is intentionally not checked into source control.

## Usage
1. Run `GLFontGen.exe`.
2. Pick a font face, weight, and whether to force fixed pitch.
3. Select the font sizes you want to export.
4. Click **Generate**.

Outputs are written to `Generated Fonts/` beside the executable:

- One `.tga` atlas per selected point size (e.g. `Consolas.16.tga`).
- A single `.tgf` metadata file with layout information for every generated height.

## Output Format
- **TGA**: 32-bit BGRA image containing packed glyphs with premultiplied alpha. Dimensions are powers of two chosen to fit the selected glyph set.
- **TGF metadata**:
  - Each font size starts with `HEIGHT <px>;`.
  - Every glyph line follows `GLYPH <x> <y> <width> <left> <right>` with optional ASCII comment.
  - `x`/`y` are the glyph origin inside the atlas, `width` is the advance width in pixels, and `left`/`right` provide side bearings.

Refer to `fontgen.cpp` if you need deeper details or want to extend the format.

## License
Released under the MIT License (see `LICENSE`).
