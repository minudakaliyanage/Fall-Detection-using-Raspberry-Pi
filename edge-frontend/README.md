# Edge AI Fall Detection - Web Dashboard

## 📋 Overview

A modern web-based monitoring dashboard for the Edge AI Fall Detection System. Built with Next.js and TypeScript, this frontend provides real-time monitoring, alert visualization, and evidence management for fall detection events.

## 📁 Project Structure

```
edge-frontend/
├── src/
│   └── app/
│       ├── page.tsx              # Main dashboard page
│       ├── layout.tsx             # Root layout
│       ├── globals.css             # Global styles
│       ├── favicon.ico             # App icon
│       └── api/                    # API routes
│           ├── screenshots/        # Screenshot retrieval
│           │   └── route.ts
│           ├── audio-files/        # Audio file retrieval
│           │   └── route.ts
│           └── alerts/             # Alert information
│               └── route.ts
├── public/
│   ├── uploads/                    # Uploaded evidence files
│   └── [icons]                     # SVG icons
├── package.json                     # Dependencies
├── next.config.ts                   # Next.js configuration
└── tsconfig.json                    # TypeScript configuration
```

## 🎯 Features

### Real-Time Monitoring
- **Live Updates** - Auto-refresh every 10 seconds
- **Detection Status** - Visual indicators for fall detection
- **Confidence Scores** - Display prediction confidence
- **Timestamp Tracking** - Real-time timestamps for all events

### Evidence Management
- **Image Gallery** - View detection screenshots
- **Audio Playback** - Listen to detected audio samples
- **Evidence Sorting** - Latest detections first
- **Evidence Filtering** - Filter by detection type

### Alert System
- **Visual Alerts** - Color-coded alert indicators
- **Alert History** - Timeline of all detections
- **Alert Details** - Detailed information for each alert
- **Notification System** - Real-time alert notifications

### User Interface
- **Modern Design** - Clean, responsive interface
- **Dark Mode Support** - Optional dark theme
- **Mobile Responsive** - Works on all devices
- **Intuitive Navigation** - Easy-to-use interface

## 🛠️ Technology Stack

- **Framework:** Next.js 15.2.4 (App Router)
- **Language:** TypeScript 5
- **Styling:** Tailwind CSS 4
- **Icons:** Lucide React
- **Cloud Integration:**
  - AWS S3 SDK
  - Azure Blob Storage SDK

## 🚀 Getting Started

### Prerequisites
- Node.js 18 or higher
- npm, yarn, pnpm, or bun
- AWS/Azure credentials (for cloud storage)

### Installation

1. **Navigate to frontend directory**
   ```bash
   cd edge-frontend
   ```

2. **Install dependencies**
   ```bash
   npm install
   # or
   yarn install
   # or
   pnpm install
   ```

3. **Configure environment variables**
   ```bash
   # Create .env.local file
   AWS_REGION=your-region
   AWS_ACCESS_KEY_ID=your-key
   AWS_SECRET_ACCESS_KEY=your-secret
   AWS_BUCKET_NAME=your-bucket
   ```

4. **Run development server**
   ```bash
   npm run dev
   # or
   yarn dev
   # or
   pnpm dev
   ```

5. **Open in browser**
   ```
   http://localhost:3000
   ```

## 📊 API Routes

### `/api/screenshots`
**GET** - Retrieve detection screenshots

**Response:**
```json
{
  "screenshots": [
    {
      "url": "https://...",
      "timestamp": "2024-01-15T10:30:00Z",
      "fallDetected": true
    }
  ]
}
```

### `/api/audio-files`
**GET** - Retrieve audio evidence files

**Response:**
```json
{
  "audios": [
    {
      "url": "https://...",
      "timestamp": "2024-01-15T10:30:00Z",
      "filename": "fall_20240115_103000.mp3"
    }
  ]
}
```

### `/api/alerts`
**GET** - Get alert information

**Response:**
```json
{
  "alerts": [
    {
      "id": "alert_123",
      "timestamp": "2024-01-15T10:30:00Z",
      "type": "fall",
      "confidence": 0.95,
      "evidence": {
        "image": "https://...",
        "audio": "https://..."
      }
    }
  ]
}
```

## 🎨 UI Components

### Dashboard Layout
- **Header** - System title and status
- **Main Panel** - Evidence display area
- **Sidebar** - Navigation and controls
- **Alert Panel** - Real-time alerts
- **Footer** - System information

### Key Components
- **Image Gallery** - Grid view of screenshots
- **Audio Player** - Playback controls
- **Alert Cards** - Visual alert indicators
- **Status Indicators** - System status display
- **Refresh Button** - Manual update trigger

## 🔄 Data Flow

### Real-Time Updates
1. Frontend polls API endpoints every 10 seconds
2. Fetches latest screenshots and audio files
3. Updates UI with new evidence
4. Displays alerts for new detections

### Evidence Display
1. Fetch evidence from cloud storage
2. Sort by timestamp (newest first)
3. Display in gallery format
4. Enable selection and viewing

## 📝 Key Files

### `src/app/page.tsx`
Main dashboard component:
- State management
- Data fetching
- UI rendering
- Event handlers

### `src/app/api/screenshots/route.ts`
Screenshot API route:
- Connect to cloud storage
- List available screenshots
- Return metadata and URLs

### `src/app/api/audio-files/route.ts`
Audio files API route:
- List audio evidence files
- Generate presigned URLs
- Return file metadata

## 🔧 Configuration

### Next.js Configuration
```typescript
// next.config.ts
export default {
  // Configuration options
}
```

### Tailwind CSS
- Custom color scheme
- Responsive breakpoints
- Component styling

## 🌐 Deployment

### Vercel Deployment
```bash
vercel deploy
```

### Self-Hosted
```bash
npm run build
npm start
```

### Environment Variables
- AWS credentials
- Azure credentials
- API endpoints
- Storage bucket names

## 📚 Dependencies

### Core
```json
{
  "next": "15.2.4",
  "react": "^19.0.0",
  "react-dom": "^19.0.0",
  "typescript": "^5"
}
```

### Cloud Integration
```json
{
  "@aws-sdk/client-s3": "^3.787.0",
  "@azure/storage-blob": "^12.27.0"
}
```

### UI
```json
{
  "lucide-react": "^0.487.0",
  "tailwindcss": "^4"
}
```

## 🎯 Features in Detail

### Auto-Refresh
- Updates every 10 seconds
- Fetches latest evidence
- Updates alert status
- Shows last update time

### Evidence Viewing
- Click to view full-size images
- Play audio files inline
- Download evidence files
- View metadata (timestamp, confidence)

### Alert Management
- Visual alert indicators
- Alert history timeline
- Filter by date/time
- Export alert data

## 🔒 Security

### API Security
- Secure cloud storage access
- Presigned URLs for temporary access
- Authentication for API routes
- CORS configuration

### Data Privacy
- Secure evidence storage
- Access control
- Data encryption
- Privacy compliance

## 📱 Responsive Design

### Breakpoints
- Mobile: < 640px
- Tablet: 640px - 1024px
- Desktop: > 1024px

### Mobile Features
- Touch-friendly interface
- Swipe gestures
- Optimized layouts
- Mobile navigation

## 🐛 Troubleshooting

### Common Issues
- **API Errors:** Check cloud storage credentials
- **No Data:** Verify evidence upload from Raspberry Pi
- **Slow Loading:** Check network connection
- **Build Errors:** Clear .next cache and rebuild

---

**Note:** This frontend provides a modern web interface for monitoring the Edge AI Fall Detection System, enabling remote monitoring and alert management.
