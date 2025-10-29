# AI Heart Health Monitor

A contactless heart health monitoring and risk prediction system that uses remote photoplethysmography (rPPG) technology to extract pulse waveform data through a device camera. This application enables non-invasive cardiovascular health assessment by analyzing facial video recordings.

## Overview

This system captures 60-second facial videos and processes them to extract heart rate data using advanced computer vision and signal processing techniques. The extracted pulse waveform data is then analyzed by an LSTM neural network to predict cardiovascular risk levels and provide personalized health insights.

## Key Features

- **Contactless Heart Rate Monitoring**: Extract pulse waveform data using rPPG technology via device camera
- **AI-Powered Risk Prediction**: LSTM-based model analyzes heart rate patterns to predict cardiovascular risk levels
- **Real-time Video Recording**: 60-second facial video capture with live camera preview
- **Historical Analysis**: Track and compare heart rate measurements over time
- **Secure Data Storage**: All health data encrypted and stored with user-level access control
- **Personalized Health Insights**: Receive tailored recommendations based on analysis results

## Technology Stack

### Frontend
- **React 18** with TypeScript for type-safe UI development
- **Vite** for fast development and optimized production builds
- **Tailwind CSS** for responsive, modern UI design
- **Lucide React** for consistent iconography

### Backend & Infrastructure
- **Supabase** for comprehensive backend services:
  - PostgreSQL database with Row Level Security (RLS)
  - Authentication system with email/password
  - Storage buckets for video files
  - Edge Functions for serverless processing
- **Supabase Client (@supabase/supabase-js)** for seamless API integration

### AI/ML Models (Deployed on Hugging Face)
- **pyVHR (Python Vital Heart Rate)**: rPPG-based pulse waveform extraction from facial videos
- **LSTM (Long Short-Term Memory) Neural Network**: Time-series analysis for cardiovascular risk prediction

### Media Processing
- **MediaRecorder API**: Native browser video recording capabilities
- **WebRTC**: Real-time camera access and video streaming

## Project Structure

```
project/
├── src/
│   ├── components/
│   │   ├── AuthForm.tsx           # User authentication UI
│   │   ├── HeartRateChart.tsx     # Real-time heart rate visualization
│   │   ├── RiskAssessment.tsx     # Risk level display and insights
│   │   └── VideoRecorder.tsx      # Camera access and recording interface
│   ├── contexts/
│   │   └── AuthContext.tsx        # Authentication state management
│   ├── lib/
│   │   └── supabase.ts            # Supabase client configuration
│   ├── pages/
│   │   ├── AnalysisPage.tsx       # Detailed analysis and results view
│   │   ├── Dashboard.tsx          # Main dashboard with recordings list
│   │   └── RecordingPage.tsx      # Video recording workflow
│   ├── services/
│   │   └── api.ts                 # API service layer for data operations
│   ├── App.tsx                    # Main application component
│   ├── main.tsx                   # Application entry point
│   └── index.css                  # Global styles and Tailwind imports
├── supabase/
│   └── migrations/
│       └── 20251008214204_create_health_monitoring_schema.sql
├── .env                           # Environment variables (see setup below)
├── package.json                   # Node.js dependencies
├── tsconfig.json                  # TypeScript configuration
├── vite.config.ts                 # Vite build configuration
└── tailwind.config.js             # Tailwind CSS configuration
```

## Database Schema

### Tables
- **users**: User profiles with health monitoring metadata
- **video_recordings**: Metadata for recorded facial videos
- **heart_rate_data**: Time-series heart rate measurements extracted from videos
- **risk_predictions**: AI-generated cardiovascular risk assessments with insights

### Security
All tables are protected with Row Level Security (RLS) policies ensuring users can only access their own data.

## Getting Started

### Prerequisites
- Node.js 18+ and npm
- A Supabase account
- Camera-enabled device for recording

### 1. Supabase Setup

#### Create a Supabase Project
1. Go to [https://supabase.com](https://supabase.com) and sign up or log in
2. Click "New Project" and fill in the required details
3. Wait for the project to be provisioned

#### Get API Credentials
1. In your Supabase project dashboard, go to **Settings** > **API**
2. Copy the following values:
   - **Project URL** (e.g., `https://xxxxx.supabase.co`)
   - **Anon/Public Key** (the `anon` `public` key)

#### Create Storage Bucket
1. In your Supabase dashboard, go to **Storage**
2. Click "Create a new bucket"
3. Name it `health-videos`
4. Set it to **Public** (so authenticated users can access their own videos)
5. Click "Create bucket"

### 2. Environment Configuration

Create a `.env` file in the project root with your Supabase credentials:

```env
VITE_SUPABASE_URL=https://your-project-id.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key-here
```

**Important**: Replace the placeholder values with your actual Supabase credentials from step 1.

### 3. Install Dependencies

```bash
npm install
```

### 4. Run Database Migrations

The database schema will be automatically applied when you first run the application. The migration file is located at:
```
supabase/migrations/20251008214204_create_health_monitoring_schema.sql
```

To manually apply migrations, use the Supabase CLI or the SQL Editor in your Supabase dashboard.

### 5. Start Development Server

```bash
npm run dev
```

The application will be available at `http://localhost:5173`

### 6. Build for Production

```bash
npm run build
```

The optimized production build will be created in the `dist/` directory.

## Usage Workflow

1. **Sign Up/Login**: Create an account or log in with existing credentials
2. **Grant Camera Permission**: Allow browser access to your camera
3. **Record Video**: Position your face in frame and record a 60-second video
4. **Processing**: The system extracts heart rate data using rPPG technology
5. **Analysis**: LSTM model analyzes patterns and generates risk assessment
6. **View Results**: Access detailed heart rate charts and personalized insights
7. **Track History**: Compare results across multiple recordings over time

## AI Models & Processing

### rPPG Heart Rate Extraction
The system uses pyVHR (deployed on Hugging Face) to analyze subtle color changes in facial skin caused by blood flow. This contactless method extracts accurate heart rate measurements without any physical sensors.

### Risk Prediction
An LSTM neural network (deployed on Hugging Face) processes the time-series heart rate data to identify patterns associated with cardiovascular health risks. The model provides:
- Risk level classification (low, medium, high)
- Numerical risk score (0-100)
- Detected anomalies and patterns
- Personalized health recommendations

## Security & Privacy

- **End-to-end encryption** for all data transmission
- **Row Level Security (RLS)** ensures data isolation between users
- **Secure authentication** with Supabase Auth
- **HIPAA-conscious design** (consult legal counsel for compliance)
- **No data sharing** with third parties

## Browser Compatibility

- Chrome/Edge 90+
- Firefox 88+
- Safari 14+
- Opera 76+

Camera access requires HTTPS (or localhost for development).

## Development Scripts

- `npm run dev` - Start development server with hot reload
- `npm run build` - Build for production
- `npm run preview` - Preview production build locally
- `npm run lint` - Run ESLint for code quality
- `npm run typecheck` - Run TypeScript type checking

## Important Notes

- Videos are stored for analysis purposes and can be deleted by users
- The system simulates AI processing in development mode (replace with actual API calls to Hugging Face models)
- Heart rate monitoring is for informational purposes only and not a substitute for professional medical advice
- Ensure adequate lighting when recording for accurate results

## Future Enhancements

- Integration with wearable device data
- Multi-user family health tracking
- Export health reports as PDF
- Integration with healthcare provider systems
- Mobile native applications (iOS/Android)
- Real-time heart rate monitoring during recording

## License

This project is for educational and demonstration purposes.

## Support

For issues, questions, or contributions, please contact the development team or open an issue in the project repository.

---

**Disclaimer**: This application is designed for informational and educational purposes only. It is not intended to diagnose, treat, cure, or prevent any disease. Always consult with qualified healthcare professionals for medical advice and treatment.
