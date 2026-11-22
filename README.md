# Lingjie-NetDisk
A free, ad-free, and pure web-based file storage and sharing application. Focused on a minimalist experience and breaking the boundaries of storage.
ZeroSpace CloudDrive is a purely front-end web application for file storage and sharing. It can be used without registration or login, supporting drag-and-drop uploads, ultra-fast instant file transfers, flat file management, and single-file or batch sharing links with optional extraction codes. The visual design features a "Cyber-Minimal Terminal" aesthetic with an ink-black background and cyber-blue accents—restrained, clean, and distraction-free.
Core Features
Zero-Barrier Access: Anonymous sessions based on device credentials allow immediate use upon opening without registration or login; data is isolated by user.
Instant Uploads: Calculates the SHA-256 hash of a file before uploading; if it matches an existing file, it instantly shows "Upload Successful" without requiring a duplicate upload.
Drag-and-Drop Uploads: Features a large drag-and-drop area where files can be uploaded by clicking or dragging; displays real-time progress bars, upload speed, and estimated time remaining.
Flat File Management: Offers both list and grid views, supports sorting by name and time, and provides download, rename, and delete functions.
Flexible Sharing:
Single-file sharing and batch sharing (select multiple files to generate one link at a time).
Optional extraction codes: freely choose between "requires extraction code" or "no extraction code needed".
Customizable expiration periods (1 day / 7 days / 30 days / permanent), with one-click copying of the link and extraction code.
Share Management: Centrally view, copy, and revoke all sharing records; batch shares display the number of files.
Theme Switching: Defaults to following the system settings, with manual toggling between dark mode (default) and a pure white minimalist mode.
Mobile Adaptation: Touch targets for upload and action buttons are no less than 48×48px.
Zero Interference: The entire site is free of ad spaces, pop-up promotions, and premium upgrade prompts.
Design Language
Style: Cyber-Minimal Terminal
Primary Color: #00F0FF Cyber Blue (used only in small areas such as buttons / icons / active states / progress bars, etc.)
Background: #0A0A0F Ink Black, with ample white space, a faint data coordinate grid, and a breathing glow effect on the upload area.
Typography: Sans-serif gothic (Heiti) for body text; monospaced JetBrains Mono is used uniformly for file sizes / timestamps / hashes / extraction codes to convey a geeky, data-driven feel.
Tech Stack
Category	Technology
Category	Technology
Front-end Framework	React 18 + TypeScript + Vite
Component Library	shadcn/ui + Radix UI + Tailwind CSS
Backend / Database	Supabase (Auth, PostgreSQL, Storage, Edge Functions)
File Storage	Supabase Storage (public bucket)
Instant Uploads	Browser-side SHA-256 hash deduplication
Directory Structure
text



├── src
│   ├── App.tsx                 # Application entry and routing
│   ├── routes.tsx              # Routing configuration
│   ├── contexts
│   │   ├── AuthContext.tsx     # Anonymous device sessions
│   │   └── ThemeContext.tsx    # Theme switching
│   ├── pages
│   │   ├── Home.tsx            # Home page: Upload + My Files
│   │   ├── Shares.tsx          # Share management page
│   │   └── SharePublic.tsx     # Share access page (for recipients)
│   ├── components
│   │   ├── file/               # File items, share/rename modals
│   │   ├── upload/             # Upload area, upload progress list
│   │   ├── layouts/            # Global navigation layout
│   │   └── ui/                 # shadcn/ui base components
│   ├── services/api.ts         # Data interaction layer (uploads/files/shares)
│   ├── hooks/useUploader.ts    # Upload task scheduling
│   ├── lib/                    # Hashing/storage path/formatting utilities
│   └── db/supabase.ts          # Supabase client
├── supabase
│   ├── migrations/             # Database migrations (table structures/RLS/RPC)
│   └── functions/anon-auth/    # Anonymous session Edge Function
└── docs
    ├── prd.md                  # Product Requirements Document
    └── DESIGN.md               # Design specifications
Local Development
Environment Requirements
bash



# Node.js ≥ 20
# npm ≥ 10
Startup Steps
bash



# 1. Install dependencies
npm i

# 2. Configure environment variables (.env)
#    VITE_APP_ID
#    VITE_SUPABASE_URL
#    VITE_SUPABASE_ANON_KEY

# 3. Code validation (this project only uses lint checks and does not start a local dev server)
npm run lint
Note: This project runs in the Miaoda platform sandbox environment, where dev / build commands are disabled; type checking and build validation are handled uniformly via npm run lint.
Backend Notes
The backend is based on Supabase, which includes:
Data Tables: profiles, files, shares, share_files, anon_credential_map
RPCs: create_share (batch create shares), resolve_share (verify extraction code and return file list), get_share_meta (share metadata), list_my_shares (my shares list)
Edge Function: anon-auth (exchanges device credentials for an anonymous session)
Storage: Public bucket files; filenames are hex-encoded to support non-ASCII characters.
Usage Flow
Open the home page, drag and drop or click to upload files, and view progress in real time.
Manage files in "My Files": download, rename, delete.
Select one or multiple files, then click "Share" (single) or "Batch Share" (multiple).
Set the expiration period in the pop-up window and choose whether an extraction code is required to generate the share link.
Recipients open the link and can download the files individually after entering the extraction code (if required).
Not Implemented in This Phase
Folder hierarchy nesting and directory management
Online preview and online editing
Multi-user collaboration and permission sharing
File version history and trash bin
Third-party cloud drive import and synchronization
License
MIT
