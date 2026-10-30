# IssueScout 🔎

### Find an open-source issue worth your time.

IssueScout is a React-based open-source issue discovery tool that helps developers find GitHub issues aligned with their programming skills, interests, and experience level.

Rather than manually searching through repositories, IssueScout combines GitHub issue search with personalized preferences and transparent heuristic scoring to help contributors discover relevant opportunities—including beginner-friendly issues.

## ✨ Features

- **Personalized issue discovery** — Search using programming skills, technical interests, experience level, and custom keywords.
- **Beginner-friendly search** — Discover issues labeled `good first issue` to make getting started with open source more approachable.
- **Live GitHub issue data** — Retrieve real issue results through an API integration designed around GitHub's Search Issues API.
- **Explainable relevance scoring** — Rank opportunities using deterministic heuristics and inspect score breakdowns and explanations.
- **Advanced filtering and sorting** — Narrow down results to find opportunities that better match your preferences.
- **Issue details** — Inspect issue information before opening the original GitHub discussion.
- **Saved issues** — Bookmark promising opportunities and revisit them later.
- **Contributor profile and preferences** — Manage skills and interests used to personalize discovery.
- **Pagination and load-more support** — Explore additional search results as needed.
- **API resilience** — Handle loading states, network errors, rate-limit information, and request cancellation.
- **Responsive interface** — A clean, focused interface designed to make issue discovery easier.

## 💡 The Problem

Finding a suitable first open-source contribution can be difficult. GitHub contains a huge number of issues, and contributors may struggle to identify opportunities that match their existing skills, interests, and experience.

IssueScout aims to reduce that friction by helping developers move from broad searches to a more focused list of relevant issues.

## 🧠 How IssueScout Works

1. **Set your preferences:** Choose your skills, interests, experience level, and optional keywords.
2. **Search GitHub issues:** Build a search query using GitHub's supported issue-search qualifiers.
3. **Normalize the results:** Convert API responses into a consistent issue structure and exclude pull requests and closed issues.
4. **Calculate relevance:** Evaluate returned issues using deterministic heuristics based on user preferences and issue information.
5. **Explore and save:** Filter, sort, inspect, and bookmark issues that look promising.
6. **Contribute:** Open the original issue on GitHub and follow the repository's contribution guidelines.

### Transparent scoring, not black-box recommendations

IssueScout's matching score is intended to help prioritize opportunities—not to predict whether a maintainer will accept a contribution. The score is generated through explicit heuristic logic, with breakdowns and explanations intended to make the ranking easier to understand.

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| React | Component-based user interface |
| Vite | Development server and production build |
| JavaScript (ES modules) | Application logic |
| Tailwind CSS | Styling and responsive layouts |
| Lucide React | Interface icons |
| GitHub REST API | Issue search and metadata |
| Vitest | Unit and component testing |
| React Testing Library | UI behavior testing |
| Vercel configuration | Frontend deployment setup |

## 🏗️ Project Structure

```text
IssueScout/
└── frontend/
    ├── public/
    ├── src/
    │   ├── assets/
    │   ├── components/
    │   │   ├── IssueCard.jsx
    │   │   ├── IssueDetailModal.jsx
    │   │   ├── FilterBar.jsx
    │   │   ├── SearchBar.jsx
    │   │   ├── PreferencesPanel.jsx
    │   │   ├── SavedIssuesDrawer.jsx
    │   │   ├── RateLimitBanner.jsx
    │   │   └── UIStates.jsx
    │   ├── context/
    │   ├── hooks/
    │   │   ├── useGitHubSearch.js
    │   │   ├── usePreferences.js
    │   │   ├── useSavedIssues.js
    │   │   └── useAuth.js
    │   ├── utils/
    │   │   ├── githubApi.js
    │   │   ├── normalization.js
    │   │   ├── scoring.js
    │   │   ├── filtering.js
    │   │   └── storage.js
    │   ├── App.jsx
    │   └── main.jsx
    ├── package.json
    ├── vite.config.js
    └── vercel.json
```

## 🚀 Getting Started

### Prerequisites

- Node.js compatible with your installed Vite version
- npm
- Git

### 1. Clone the repository

```bash
git clone <YOUR_REPOSITORY_URL>
cd IssueScout/frontend
```

Replace `<YOUR_REPOSITORY_URL>` with the actual URL of your GitHub repository.

### 2. Install dependencies

```bash
npm install
```

### 3. Configure the API URL

Create a `.env` file in the `frontend/` directory:

```env
VITE_API_BASE_URL=http://localhost:5000
```

The frontend API client uses this variable to determine where to send issue-search requests. If it is omitted, the client defaults to relative API paths, which require a same-origin API or a correctly configured development proxy.

**Important:** The supplied project structure does not show the Express backend. You will need a compatible backend running locally or a deployed API endpoint for searches to work through this configuration.

Do not put private API tokens or other secrets in `VITE_` variables because Vite exposes them to client-side code.

### 4. Start the development server

```bash
npm run dev
```

Open the local URL printed by Vite, typically `http://localhost:5173`.

## 🧪 Testing and Quality Checks

IssueScout includes tests for important application utilities and UI workflows.

Run the test suite:

```bash
npm test
```

Create a production build:

```bash
npm run build
```

Run lint checks:

```bash
npm run lint
```

The project includes tests for GitHub API behavior, issue normalization, scoring, filtering, browser storage, preferences, and component workflows. Run these commands locally to verify the current state of the project before release.

## 🔌 GitHub API Integration

The GitHub API client builds search queries using qualifiers such as `is:issue` and `is:open`, alongside selected skills, keywords, and labels.

The implementation also includes:

- Pagination support
- Client-side response caching with a three-minute time-to-live
- Rate-limit header parsing
- Request cancellation and protection against outdated search responses
- Consistent issue normalization
- Filtering out pull requests and closed issues
- Network and API error states

The current client is configured for a backend API integration. Verify that the backend is present, correctly configured, and reachable before deploying the complete application.

Official documentation:

- [GitHub Search Issues and Pull Requests API](https://docs.github.com/en/rest/search/search)
- [GitHub REST API rate limits](https://docs.github.com/en/rest/using-the-rest-api/rate-limits-for-the-rest-api)

## 🌐 Deployment

The repository includes a Vercel configuration for the Vite frontend.

For a frontend-only deployment:

1. Import the repository into Vercel.
2. Set the project root directory to `frontend` if that matches the repository layout.
3. Use `npm run build` as the build command.
4. Set `dist` as the output directory.
5. Configure `VITE_API_BASE_URL` to point to the deployed API service.
6. Deploy and verify the frontend and a real issue-search request.

The frontend deployment alone does not provide the Express API. If the backend is maintained separately, deploy it as its own service and configure its CORS policy and frontend origin appropriately.

Add a live demo URL to this README only after the deployed application has been tested.

## 🔭 Future Improvements

- Complete, documented backend deployment
- More detailed explanations of individual matching signals
- Repository activity and maintenance indicators
- Better detection of stale or inactive issues
- Improved relevance evaluation using contributor feedback
- Optional GitHub authentication where needed
- Cross-device saved issues and synchronized preferences
- Contribution progress tracking

## 🤝 Contributing

Contributions and suggestions are welcome.

1. Fork the repository.
2. Create a branch for your changes.
3. Implement your feature or fix.
4. Add or update tests.
5. Run the test suite and production build.
6. Open a pull request describing your changes.

Please do not commit `.env` files containing secrets or access tokens.

## 📄 License

Add a `LICENSE` file to specify how others may use, modify, and distribute this project.

---

**IssueScout — helping developers find their next meaningful open-source contribution.**
