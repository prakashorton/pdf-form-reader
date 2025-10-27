# PDF Form Reader

A modern web application for extracting and displaying form fields from PDF documents with interactive field highlighting.

## 🚀 Live Demo

- **Frontend**: [https://prakashorton.github.io/pdf-form-reader/](https://prakashorton.github.io/pdf-form-reader/)
- **Backend**: Deploy with one click ↓

[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy?repo=https://github.com/prakashorton/pdf-form-reader)

## Features

- 📄 **PDF Upload** - Drag & drop or click to upload PDF files
- 👁️ **PDF Viewer** - Interactive PDF viewer with zoom controls
- 📝 **Field Extraction** - Automatic extraction of form fields and values
- 🎯 **Interactive Highlighting** - Click form fields to highlight corresponding areas in PDF
- 📋 **Copy to Clipboard** - Easy copy functionality for each field
- 🎨 **Modern UI** - Clean, responsive design with smooth animations

## Tech Stack

### Frontend
- **React 19.1.1** - UI framework
- **TypeScript 5.9.3** - Type safety
- **Vite 7.1.7** - Fast build tool
- **TailwindCSS 3.4.18** - Styling
- **Framer Motion 12.23.24** - Animations
- **PDF.js** - PDF rendering

### Backend
- **Node.js & Express** - Server
- **pdf-lib** - PDF manipulation
- **pdfjs-dist** - Text extraction
- **Tesseract.js** - OCR for image-based PDFs
- **Multer** - File upload handling

## Installation

### Prerequisites
- Node.js 18+ 
- npm or yarn

### Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd sample-ai
   ```

2. **Install frontend dependencies**
   ```bash
   cd pdf-form-reader
   npm install
   ```

3. **Install backend dependencies**
   ```bash
   cd server
   npm install
   ```

4. **Configure environment (optional)**
   ```bash
   cd server
   cp .env.example .env
   # Edit .env if needed
   ```

## Running the Application

### Development Mode

1. **Start the backend server** (Terminal 1)
   ```bash
   cd pdf-form-reader/server
   npm start
   ```
   Server runs on: http://localhost:3001

2. **Start the frontend** (Terminal 2)
   ```bash
   cd pdf-form-reader
   npm run dev
   ```
   App runs on: http://localhost:5173/pdf-form-reader/

3. **Open browser**
   Navigate to: http://localhost:5173/pdf-form-reader/

## Usage

1. **Upload PDF**
   - Click "Choose PDF File" or drag & drop a PDF
   - PDF appears in left pane

2. **View Extracted Fields**
   - Form fields appear in right pane
   - Values are automatically extracted

3. **Interact with Fields**
   - Click any field in the right pane
   - Corresponding area highlights in PDF viewer
   - Click copy icon to copy field value

## Extraction Methods

The application uses multiple extraction methods:

1. **Text Extraction** (Primary)
   - Fast extraction for PDFs with selectable text
   - Pattern matching for known field formats

2. **OCR** (Fallback)
   - For image-based or scanned PDFs
   - Uses Tesseract.js for text recognition
   - Requires additional setup for full functionality

3. **Sample Data** (Demo)
   - Returns sample fields for demonstration
   - Shows UI functionality without real extraction

## Supported Fields

- Post Office
- Date (ddmmyy format)
- CIF ID
- Full Name
- Primary Account ID
- Email ID
- PAN Number
- Mobile Number
- Internet Banking Required (Yes/No)

## Project Structure

```
sample-ai/
├── pdf-form-reader/
│   ├── src/
│   │   ├── components/
│   │   │   ├── PDFViewer.tsx      # PDF rendering component
│   │   │   └── FileUpload.tsx     # Upload component
│   │   ├── store/
│   │   │   └── formStore.ts       # State management
│   │   ├── App.tsx                # Main app component
│   │   └── main.tsx               # Entry point
│   ├── server/
│   │   ├── index.js               # Express server
│   │   ├── .env.example           # Environment template
│   │   └── package.json           # Server dependencies
│   ├── package.json               # Frontend dependencies
│   └── vite.config.ts             # Vite configuration
├── .gitignore
└── README.md
```

## API Endpoints

### POST /api/extract-pdf-fields
Upload PDF and extract form fields

**Request:**
- Method: POST
- Content-Type: multipart/form-data
- Body: PDF file

**Response:**
```json
{
  "success": true,
  "fields": [
    {
      "name": "Post Office",
      "value": "Delhi GPO",
      "type": "text"
    }
  ],
  "totalFields": 9,
  "extractionMethod": "text-pattern-matching"
}
```

### GET /api/health
Health check endpoint

**Response:**
```json
{
  "status": "ok",
  "message": "Adobe PDF Extract API server is running"
}
```

## Configuration

### Environment Variables

Create `pdf-form-reader/server/.env`:

```env
# Server Configuration
PORT=3001

# Optional: Google Gemini API Key (for AI extraction)
GEMINI_API_KEY=your_api_key_here
```

## Deployment

### Frontend (Vite)

```bash
cd pdf-form-reader
npm run build
# Deploy dist/ folder to your hosting service
```

### Backend (Node.js)

```bash
cd pdf-form-reader/server
# Deploy to Node.js hosting (Heroku, Railway, etc.)
```

### Environment Setup

Make sure to set environment variables on your hosting platform:
- `PORT` - Server port (default: 3001)
- `GEMINI_API_KEY` - (Optional) For AI-powered extraction

## Troubleshooting

### No fields extracted
- Check if PDF has selectable text
- Try a different PDF
- Check server logs for errors

### OCR not working
- OCR requires additional setup
- Currently returns sample data for image-based PDFs
- For full OCR, install GraphicsMagick or ImageMagick

### Server connection errors
- Ensure backend is running on port 3001
- Check CORS configuration
- Verify API_URL in frontend code

## Future Enhancements

- [ ] Full OCR implementation with GraphicsMagick
- [ ] Support for multi-page PDFs
- [ ] Custom field mapping
- [ ] Export to JSON/CSV
- [ ] Batch processing
- [ ] Field validation
- [ ] User authentication
- [ ] Cloud storage integration

## License

MIT

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Support

For issues and questions, please open an issue on GitHub.

