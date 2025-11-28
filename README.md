# NativeFlip 3D — Hardcover Edition

NativeFlip 3D is a high-fidelity, interactive 3D PDF reader for the web. It converts standard PDFs into a realistic hardcover book with physics-based page turns, dynamic lighting, and a professional annotation + AI-assisted study toolset.

## Key Features
- Realistic 3D hardcover model with leather texture and spine
- Physics-based page turning with bending deformation
- Spread / single-page focus (left/right) camera modes
- High-DPI page rendering and anisotropic filtering for crisp text
- Annotation suite: pen (multi-color), highlighter, eraser, sticky notes, and typed text
- Text selection mapped from 3D surface to PDF text extraction and copy-to-clipboard
- Persistent annotations tied to page coordinates
- Magnifier lens for reading fine print
- Scrubbing / speed-flip widget (fanning) to quickly preview pages
- Optional AI Assistant (Gemini) for summaries, quizzes and explanations

## Live Preview
Serve locally (required due to browser file and worker restrictions) and open:
http://localhost:8000

## Quick start

1. Clone the repo
   git clone https://github.com/yourusername/nativeflip-3d.git
   cd nativeflip-3d

2. Serve the folder with a simple static server:
   - Python:
     python -m http.server 8000
   - Node (http-server):
     npx http-server --cors -p 8000

3. Open your browser and navigate to:
   http://localhost:8000

4. Click "Open PDF" and select a `.pdf` file.

## Prerequisites
- Modern browser with WebGL2 support (Chrome, Edge, Firefox)
- Optional: API key for Google Gemini to enable AI Assistant (see below)

## Configuration
Open `index.html`, find the `CONFIG` object near the top and adjust parameters:
- bookWidth, bookHeight — page size in scene units
- maxThickness, coverThickness — visual thickness of the block and cover
- spineColor, coverColor, paperColor — material colors
- flipSpeed — automatic page-turn speed
- fanningInterval — speed for scrubbing/fanning behavior

AI key:
- Locate `const apiKey = "";` near the bottom of `index.html` and insert your API key.
- Note: For production, proxy requests through a backend to avoid exposing keys client-side.

## File / Asset Notes
- Uses Three.js r128, PDF.js 2.16 and Tween.js CDN builds.
- All page rendering uses `CanvasTexture` and is cached in-memory; textures may be disposed to free GPU memory when re-rendered.
- The magnifier reads pixels from the main WebGL canvas (renderer created with preserveDrawingBuffer=true).

## Development & Debugging
- Use the browser console to inspect errors and renderer state.
- To speed up texture preloading during development, reduce `CONFIG.fanningInterval` or adjust the TextureScheduler bufferSize in `index.html`.
- If pages appear blank, confirm PDF.js worker URL and that the site is served over HTTP(S) (file:// will fail).

## Troubleshooting
- "PDF not loading": Ensure the file type is `application/pdf` and you're serving from a local server.
- "Text selection inaccurate": PDF text extraction depends on PDF structure and `getTextContent()` accuracy; complex layouts may yield imperfect bounds.
- "AI requests failing": Check API key presence, quota, and that network requests to Google APIs are allowed.

## Contributing
- Fork, create a feature branch, and submit a pull request.
- Keep changes modular and include visual demos/screenshots for UI or rendering changes.
- For large feature work (new rendering or AI flows), open an issue to discuss design first.

## License
MIT — see LICENSE file.

## Contact
Project maintained in this repository. For questions or help,