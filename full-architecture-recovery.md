## Full Architecture Recovery

### Purpose
Reverse engineer the backend + frontend structure of the NovelVision AI application, identify outdated patterns, and plan a clean, modern structure that reflects actual features and project growth.

### Investigation Framework

#### 1. User-Facing Frontend Analysis
- **Current Pages Inventory:** Map all public pages in `/root/` directory
- **Feature Exposure:** Identify which core features are (not) exposed in the UI
- **UX Patterns:** Document inconsistent or broken UX patterns
- **Content Audit:** List outdated or misleading content
- **Asset Organization:** Analyze CSS, JS, and media asset organization

#### 2. Backend Logic Documentation
- **Firebase Modules:** Map all Firebase dependencies and usage patterns
- **API Endpoints:** Document active endpoints, their purpose, and authentication
- **Legacy Code:** Identify deprecated or unused backend components
- **Runtime Environment:** Document Hetzner VPS configuration and deployment

#### 3. SDK & Agent Integration
- **FAL.ai Integration:** Map image/video generation routes and authentication flow
- **OpenRouter Usage:** Document LLM integration points
- **Iframe Modules:** Analyze embedding patterns for SDK modules
- **Permissions & Keys:** Document how API keys/credentials are managed

#### 4. Routing & Redirect Logic
- **URL Structure:** Map current URL patterns and SEO strategy
- **.htaccess Rules:** Document all rewrite and redirect rules
- **Static Mappings:** Analyze hardcoded route definitions
- **Fallback Behavior:** Document 404 handling and error pages

### Expected Deliverables
- **Architecture Map:** Visual representation of current system components
- **Page Structure Blueprint:** Proposed organization for a refactored frontend
- **Migration Plan:** Step-by-step approach for landing and feature pages
- **Technical Debt Register:** Prioritized list of code issues to address

### Current Status: IN PROGRESS

### Current Architecture Diagram

```
                 +--------------------------------+
                 |      novelvisionai.art         |
                 +--------------------------------+
                 |                                |
                 v                                v
   +------------------------+        +-------------------------+
   |    Landing Pages       |        |    Application Pages    |
   | (Root Directory)       |        |                         |
   +------------------------+        +-------------------------+
   | - index.html           |        | - pages/auth.html       |
   | - home.html            |        | - pages/settings.html   |
   | - faq.html             |        | - pages/index.html      |
   | - contact.html         | -----> | - pages/story-*.html    |
   | - requirements.html    |        | - writer_workspace/     |
   | - instructions.html    |        |   writing_working_space |
   +------------------------+        +-------------------------+
                                      |            ^
                                      v            |
   +------------------------+        +-------------------------+
   |  Firebase Integration  |<------>|    API Proxies (PHP)    |
   | (Authentication/DB)    |        | (/api/ directory)       |
   +------------------------+        +-------------------------+
   | - initFirebase.js      |        | - chat_completion.php   |
   | - auth.js              |        | - falai_*.php           |
   | - db.js                |        | - error_logger.php      |
   | - firebaseSettings.js  |        +------------+------------+
   +------------------------+                     |
                                                  v
   +------------------------+        +-------------------------+
   |  Video SDK (iframe)    |        |      External APIs      |
   | (Hetzner VPS)          |<------>| (OpenRouter, FAL.ai)    |
   +------------------------+        +-------------------------+
   | - Next.js App          |        | - LLM Services          |
   | - App Router           |        | - Image Generation      |
   | - /api/fal Proxy       |        | - Authentication        |
   +------------------------+        +-------------------------+
```

### Proposed Architecture Blueprint

```
                        +---------------------------------------+
                        |        novelvisionai.art              |
                        +---------------------------------------+
                        |                                       |
         +------------------------+       +------------------------+
         |                        |       |                        |
         v                        v       v                        v
+------------------+    +------------------+    +------------------+
|  Public Pages    |    |  Dashboard Pages |    |    App Pages     |
| (Marketing Site) |    | (User Account)   |    | (Writing Tools)  |
+------------------+    +------------------+    +------------------+
| - Home           |    | - Login/Register |    | - Story Editor   |
| - Features       |    | - Dashboard      |    | - Character Gen. |
| - Pricing        |    | - Settings       |    | - Plot Structure |
| - Documentation  |    | - API Keys       |    | - Image Gen.     |
| - FAQ            |    | - Usage Stats    |    | - Video Studio   |
| - Contact        |    | - Account        |    | - Publishing     |
+------------------+    +------------------+    +------------------+
         |                      |                       |
         v                      v                       v
+------------------+    +------------------+    +------------------+
|  Shared Layouts  |    | Shared Components|    | Common Services  |
+------------------+    +------------------+    +------------------+
| - Header/Footer  |    | - Modal System   |    | - Form Controls  |
| - Navigation     |    | - UI Components  |    | - UI Components  |
| - Theme Provider |    | - UI Components  |    | - API Client     |
+------------------+    +------------------+    +------------------+
                                |
                                v
                      +------------------+
                      |  API Gateway     |
                      | (Firebase/PHP)   |
                      +------------------+
                      | - Auth           |
                      | - Endpoints      |
                      | - Proxy Services |
                      +------------------+
                         |         |
           +-------------+         +------------+
           |                                    |
           v                                    v
+------------------+                  +------------------+
|   External APIs  |                  |   Video SDK      |
|  (Via Proxies)   |                  | (iframe Protocol)|
+------------------+                  +------------------+
| - OpenRouter     |                  | - Secure Comm.   |
| - FAL.ai         |                  | - Key Management |
| - Other Services |                  | - Story Data     |
+------------------+                  +------------------+
```

### Migration Plan

#### Phase 1: Foundation Reorganization

**1. Public Landing Pages Restructuring**
- Create a unified public pages structure:
  - Move landing pages into `/public/` directory
  - Implement consistent header/footer components
  - Fix broken links and navigation paths
  - Create a proper home page showcasing all features
  - Setup proper auth flow redirects

**2. Application Entry Point Consolidation**
- Create a clear "app dashboard" as the post-login landing page
- Integrate all features into a unified dashboard:
  - Story project management
  - Settings and user profile
  - Image generation access
  - Video production feature links
  - API key management

**3. API Gateway Standardization**
- Refactor the PHP proxy system:
  - Implement a unified API gateway
  - Standardize error handling and response formats
  - Create consistent authentication middleware
  - Document all endpoints
  
**4. Authentication Flow Consistency**
- Standardize auth patterns across the application
- Create proper auth guards for all protected routes
- Implement unified localStorage and Firestore sync
- Add proper session management and security

#### Phase 2: Feature Integration & UX Improvement

**1. Writing Workspace Enhancements**
- Integrate the writing workspace into the main application:
  - Move from `/writer_workspace/` to `/app/editor/`
  - Maintain feature parity with current implementation
  - Improve UI/UX using modern component patterns
  
**2. Media Generation Hub**
- Create a dedicated media generation section:
  - Unified UI for image generation
  - Video SDK integration in native context
  - Consolidated asset management
  - Gallery view for all generated media
  
**3. SDK Integration Improvement**
- Improve the Video SDK integration:
  - Replace iframe with more robust integration
  - OR improve postMessage protocol with standardized functions
  - Implement better error handling and fallbacks
  - Create consistent look and feel

**4. Settings & Preferences**
- Create a comprehensive settings dashboard:
  - User account management
  - API key management
  - Notification preferences
  - Theme and UI preferences
  - Usage statistics

#### Phase 3: Infrastructure & Performance

**1. Build System Implementation**
- Implement a modern build system:
  - Use Webpack or Vite for asset bundling
  - Set up proper minification and optimization
  - Implement CSS preprocessing
  - Add code splitting and lazy loading
  
**2. Deployment Pipeline**
- Create a proper CI/CD pipeline:
  - Automated testing
  - Staged deployments
  - Environment-specific configuration
  - Rollback capabilities
  
**3. Performance Optimization**
- Optimize for speed and resource usage:
  - Implement proper asset caching
  - Optimize image loading and delivery
  - Improve client-side performance
  - Reduce API call overhead

**4. Documentation & Monitoring**
- Implement comprehensive documentation:
  - API documentation
  - User guides
  - Developer documentation
  - Setup monitoring and error tracking

### Technical Debt Register

*Priority: Critical (C), High (H), Medium (M), Low (L)*

| ID | Issue | Priority | Impact | Resolution |
|----|-------|----------|--------|------------|
| TD01 | Inconsistent auth flow between pages | C | Security, UX | Standardize auth checks across all protected pages |
| TD02 | Broken navigation paths | C | UX | Fix all links and create consistent navigation |
| TD03 | Scattered API key management | H | Security | Centralize API key storage and retrieval |
| TD04 | iframe-based SDK integration fragility | H | Stability | Implement robust communication protocol |
| TD05 | Lack of proper error handling | H | Reliability | Standardize error handling across all services |
| TD06 | PHP proxy security concerns | H | Security | Add proper input validation and security headers |
| TD07 | Duplicated code across components | M | Maintainability | Extract shared code into common libraries |
| TD08 | Inconsistent UI patterns | M | UX | Implement design system with reusable components |
| TD09 | Missing feature documentation | M | Usability | Create comprehensive user documentation |
| TD10 | Lack of testing | M | Quality | Implement automated testing for critical paths |
| TD11 | Manual deployment process | M | DevOps | Create automated deployment pipeline |
| TD12 | Mixed CSS approaches | L | Maintainability | Standardize on a single CSS methodology |
| TD13 | Outdated dependencies | L | Security | Audit and update all dependencies |
| TD14 | Inadequate logging | L | Debugging | Implement structured logging and monitoring |
| TD15 | No analytics integration | L | Business | Add proper analytics to track usage patterns |

### Investigation Notes

#### Initial Application Structure Analysis

**1. Top-Level Directory Structure**
- The application is spread across multiple directories without a clear separation of concerns
- Key directories include:
  - `/pages/`: Contains authenticated app pages (auth.html, settings.html, story-outline.html, etc.)
  - `/writer_workspace/`: Contains the main writing interface (writing_working_space.html)
  - `/js/`: Contains frontend JavaScript logic
  - `/api/`: Contains PHP API endpoints for external services
  - `/firebase_core/`: Contains Firebase integration for auth and data storage
  - `/video-starter-kit/`: Contains the Next.js SDK for AI video generation

**2. Frontend Page Structure**
- Landing pages are in the root directory (home.html, index.html, faq.html, contact.html)
- Main app pages are in the `/pages/` directory
- The landing pages don't accurately reflect the app's current features and capabilities
- Authentication is handled via Firebase (firebase_core/auth.js)

**3. Backend Structure**
- Firebase is used for authentication and data storage
- PHP API endpoints in `/api/` directory proxy requests to external services:
  - `falai_image_generation.php`, `falai_status.php`, etc. for FAL.ai integration
  - `chat_completion.php` for OpenRouter/OpenAI integration
- No traditional server-side application framework is used

**4. SDK & External Services**
- AI Video SDK (`/video-starter-kit/`) is a standalone Next.js application
  - Deployed via `deploy_sdk.sh` to a Hetzner VPS
  - Uses a custom proxy (`/api/fal/route.ts`) for FAL.ai API calls
- Image generation via FAL.ai is integrated in the main app through PHP proxies

**5. Routing & URL Structure**
- Simple redirects in `.htaccess` for basic routing
- `index.html` redirects to `home.html`
- Authentication redirects handled by Firebase (firebase_core/auth.js)

**6. Key Observations**
- The application evolved from a simple single-page app to a more complex system
- The frontend doesn't coherently present all available features
- Multiple authentication patterns and storage mechanisms coexist
- The Video SDK is completely separate from the main application architecture

#### Detailed Component Analysis

**1. Authentication Flow**
- Firebase Authentication handles user login/registration/password reset
- Auth methods supported: Email/Password and Google Sign-In
- `auth.js` module provides core authentication functions:
  - `loginWithEmail()`, `registerWithEmail()`, `loginWithGoogle()`, `logoutUser()`
  - `getCurrentUser()`, `getCurrentUserId()`, `onAuthStateChange()`
- User persistence in Firestore:
  - Creates user document on registration
  - Stores user-specific settings (API keys, preferences)
- Auth integration with the rest of the app:
  - `loadSettings()` function loads user settings from Firestore to localStorage
  - API keys stored in both Firestore and localStorage for persistence

**2. API Proxy Architecture**
- PHP-based API proxy layer handles external API calls
- **Core API endpoints:**
  - `/api/chat_completion.php`: Proxies requests to OpenRouter for LLM features
  - `/api/falai_image_generation.php`: Proxies requests to FAL.ai for image generation
  - `/api/falai_status.php`: Polls FAL.ai for status updates on image generation
  - `/api/falai_schnell.php`: Handles quick image generation requests
- **API Key Management:**
  - API keys are read from request headers
  - `X-API-KEY` header for OpenRouter
  - `Authorization: Key {key}` header for FAL.ai
  - Keys are originally stored in Firestore but cached in localStorage

**3. Video SDK Integration**
- Next.js-based Video SDK running independently on Hetzner VPS
- Integration with main app:
  - Loaded via iframe in `writer_workspace/writing_working_space.html`
  - Uses postMessage API for communication between main app and SDK
  - Implemented in `js/ai_visual_studio/index.js`
- **Communication Pattern:**
  - SDK requests data (user ID, API key, story content) via postMessage
  - Parent app responds with requested data
  - Origin validation ensures security (only accepts messages from trusted domains)
- **Deployment:**
  - Deployed to Hetzner VPS via `deploy_sdk.sh`
  - Uses PM2 for process management
  - Nginx as reverse proxy with SSL (Let's Encrypt)

**4. API Key Flow**
- API keys are obtained from the user via settings page
- Key storage flow:
  1. User enters API keys in `/pages/settings.html`
  2. Keys are stored in Firestore linked to user ID
  3. Keys are also cached in localStorage for persistence
  4. Frontend JS reads keys from localStorage when making API requests
  5. PHP proxy endpoints extract keys from request headers
  6. Video SDK receives keys via postMessage from parent app

**5. Data Storage Architecture**
- **Firebase Firestore:**
  - Primary cloud storage for user data
  - Stores user profiles, API keys, premium status
  - Collection structure: `users/{userId}`
- **LocalStorage:**
  - Used for caching Firestore data
  - Stores story content, API keys, and user preferences
  - Facilitates offline capabilities and reduces Firestore reads

#### Feature Integration Analysis

**1. Story Writing Workspace**
- Core writing interface in `writer_workspace/writing_working_space.html`
- Integrates with multiple AI services:
  - OpenRouter/OpenAI for text generation
  - FAL.ai for image generation
  - SDK for video generation
- Data flow:
  - Story content stored in localStorage
  - API requests sent to PHP proxy endpoints
  - AI-generated content displayed in the UI

**2. Image Generation**
- Implemented in `writer_workspace/js/imageGeneration.js`
- Uses FAL.ai's FLUX model for image generation
- Process flow:
  1. User inputs prompt
  2. Request sent to `/api/falai_image_generation.php`
  3. PHP proxy forwards request to FAL.ai
  4. Polling `/api/falai_status.php` for generation status
  5. Displaying generated images in the UI

**3. Video Generation**
- Handled entirely by the Video SDK
- Integration points:
  - "AI Visual Studio" button in writing workspace
  - iframe loads SDK from `https://sdk.novelvisionai.art/app`
  - Story content sent to SDK via postMessage
- No direct API calls from main app to video generation APIs

#### Landing Page & Public UI Analysis

**1. Public Pages Inventory**
- **Root directory landing pages:**
  - `index.html`: Simple redirect to home.html
  - `home.html`: Main landing page with feature overview
  - `faq.html`: Frequently asked questions about the app
  - `contact.html`: Contact form and feature voting
  - `requirements.html`: System requirements and setup instructions
  - `instructions.html`: Detailed usage instructions
- **Authentication-related:**
  - `pages/auth.html`: Firebase authentication (login/register)
- **Application pages:**
  - `pages/settings.html`: User settings and API key management
  - `pages/index.html`: Story creation wizard starting point
  - `pages/story-outline.html`: Story outline creation
  - `pages/character_setup.html`: Character development
  - `pages/story-setting.html`: Story setting/world creation
  - `writer_workspace/writing_working_space.html`: Main writing interface

**2. Navigation & User Flow Issues**
- **Inconsistent navigation paths:**
  - Public pages link to `auth.html` (wrong path - should be `pages/auth.html`)
  - No clear flow from landing pages to actual application
  - Disjointed experience between marketing pages and application
- **Multiple entry points:**
  - Public pages in root directory
  - Application pages in `/pages/` directory
  - Writing interface in separate `/writer_workspace/` directory
- **Authentication issues:**
  - Public pages don't check auth status correctly
  - No consistent header/navigation between public and application pages

**3. Content & Messaging Analysis**
- **Feature representation gaps:**
  - Video SDK (AI Visual Studio) is not mentioned on landing pages
  - Landing pages focus on text generation and basic image generation
  - Advanced features are not adequately showcased
- **Outdated information:**
  - API setup instructions reference potentially outdated services
  - Some UI screenshots don't match current application design
- **Incomplete user guidance:**
  - No clear explanation of the relationship between different app sections
  - Missing guidance on video generation capabilities
  - No cohesive documentation of the full application workflow

**4. UI Pattern Inconsistencies**
- **Visual design inconsistencies:**
  - Different UI frameworks between landing pages and application pages
  - Inconsistent header/footer implementation
  - Varying color schemes and component styles
- **Component pattern differences:**
  - Public pages use direct Tailwind CSS
  - Application uses a mix of custom components
  - Different modal and form patterns across sections
- **Responsive design issues:**
  - Some sections not fully responsive
  - Inconsistent mobile navigation treatment
  - Different breakpoint patterns across sections

**5. Asset Organization Problems**
- **CSS structure issues:**
  - Mix of inline styles, shared CSS, and Tailwind utility classes
  - No consistent CSS organization pattern
  - Duplicated styles across pages
- **JavaScript organization:**
  - Multiple overlapping utility scripts
  - No clear modular structure for functionality
  - Inconsistent loading patterns (module vs. traditional)
- **Media assets:**
  - Images scattered across multiple directories
  - No standardized naming convention
  - Mixture of static and dynamically generated assets

#### Critical Architectural Gaps

**1. Frontend-Backend Separation**
- No clear separation between frontend and backend components
- PHP files mixed with frontend HTML/JS
- No unified API gateway or service layer

**2. Authentication Integration**
- Firebase auth is implemented but not consistently enforced
- Multiple auth check patterns exist
- Token handling varies across components

**3. Feature Discoverability**
- Core features hidden in deeply nested UI
- No cohesive showcase of all capabilities
- Fragmented user journey across multiple sections

**4. Developer Experience**
- No consistent build process or toolchain
- Mixed deployment patterns (manual vs. script)
- Limited code organization and documentation

#### Architectural Issues & Technical Debt

**1. Frontend Structure Issues**
- Landing pages don't reflect actual app capabilities
- Inconsistent UI patterns between landing pages and app pages
- No clear navigation between features
- Multiple separate page hierarchies (`/`, `/pages/`, `/writer_workspace/`)

**2. Backend Structure Issues**
- No proper API gateway or backend framework
- Simple PHP proxies instead of structured API layer
- Dependency on Firebase for auth but no cohesive backend architecture
- Mixed storage patterns (Firestore + localStorage)

**3. Integration Challenges**
- Video SDK is completely separate from main app
- iframe + postMessage communication is brittle
- Duplicate code for API key management across components
- No centralized configuration management

**4. Deployment Complexity**
- Split deployment between main web server and Hetzner VPS
- Manual deployment process via shell script
- No CI/CD pipeline for automated testing and deployment
- Complex proxy configuration between services

**Next Steps**:
1. Create visual architecture map of current components
2. Design new page structure for cohesive user experience
3. Identify critical refactoring priorities
4. Develop migration plan for frontend reorganization 