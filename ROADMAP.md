# 16x Writer Development Roadmap

Web platform for AI-assisted writing and editing of blog posts.

## Overview

16x Writer is an AI-powered writing platform that helps users create high-quality blog posts by leveraging:

- **Source Library**: News articles, Reddit posts, X posts for content ideas
- **Reference Library**: Example blog posts for structure and style guidance
- **Prompt Library**: AI prompts for drafting and editing
- **Post Editor**: AI-assisted writing with version control and diff viewing

## Development Workflow

1. **Task Planning**

- Study the existing codebase and understand the current state
- Update `ROADMAP.md` to include the new task
- Priority tasks should be inserted after the last completed task

2. **Task Creation**

- Study the existing codebase and understand the current state
- Create a new task file in the `/tasks` directory
- Name format: `XXX-description.md` (e.g., `001-db.md`)
- Include high-level specifications, relevant files, acceptance criteria, and implementation steps
- Refer to last completed task in the `/tasks` directory for examples. For example, if the current task is `012`, refer to `011` and `010` for examples.
- Note that these examples are completed tasks, so the content reflects the final state of completed tasks (checked boxes and summary of changes). For the new task, the document should contain empty boxes and no summary of changes. Refer to `000-sample.md` as the sample for initial state.

3. **Task Implementation**

- Follow the specifications in the task file
- Implement features and functionality
- Update step progress within the task file after each step
- Stop after completing each step and wait for further instructions

4. **Roadmap Updates**

- Mark completed tasks with ✅ in the roadmap
- Add reference to the task file (e.g., `See: /tasks/001-db.md`)

## Development Phases

### Phase 1: Content Management Foundation ✅

- **Task 001: Database Schema** ✅ - Complete
  - See: `/tasks/001-db.md`
  - Implemented 5 core tables: `context`, `prompts`, `posts`, `post_versions`, `post_context`
  - Added UUID primary keys and proper relationships
  - Created CRUD operations and seed data
  - Generated migration files

### Phase 2: Core Writing Experience (MVP) ✅

- **Task 002: Source Library UI** ✅ - Complete

  - See: `/tasks/002-source-library.md`
  - ✅ List view with filtering and search functionality
  - ✅ Add/edit source forms with comprehensive metadata fields
  - ✅ Grid/list view toggle for source display
  - ✅ Source management with CRUD operations
  - ✅ API endpoints for source management (`/api/sources`)
  - ✅ Real-time source list with SWR for data fetching
  - ✅ Delete confirmation dialogs and optimistic updates

- **Task 003: End-to-End Testing** ✅ - Complete

  - See: `/tasks/003-e2e-testing.md`
  - ✅ Playwright setup with TypeScript support
  - ✅ Authentication flow tests (sign up, login)
  - ✅ Source library CRUD tests
  - ✅ Test environment configuration
  - ✅ CI/CD integration

- **Task 004: Refactor Sources to Generic Context Components** ✅ - Complete

  - See: `/tasks/004-source-refactor-context.md`
  - ✅ Created generic `/api/context/*` routes with contextType parameter
  - ✅ Built reusable context components (ContextList, ContextForm, ContextCard, ContextDetail)
  - ✅ Migrated all source pages to use generic components with `contextType="source"`
  - ✅ Removed old source-specific components and API routes
  - ✅ Maintained all existing functionality with improved maintainability
  - ✅ Simple conditional logic for context-specific features

- **Task 005: Reference Library UI** ✅ - Complete

  - See: `/tasks/005-reference-library-implementation.md`
  - ✅ Reference list view with search and filtering functionality
  - ✅ Add/edit reference forms with title, content, and notes fields
  - ✅ Reference detail view and management
  - ✅ Navigation integration with BookOpen icon
  - ✅ Comprehensive E2E test suite with 12 passing tests
  - ✅ Generic context components reused for references

- **Task 006: Post Creation Flow** ✅ - Complete

  - See: `/tasks/006-post-creation-flow.md`
  - ✅ Post management pages with list view, filtering, and search
  - ✅ Post cards with status indicators and metadata display
  - ✅ API endpoints for post CRUD operations
  - ✅ Post creation form with prompt and context selection
  - ✅ AI-powered initial draft generation using send-prompt library
  - ✅ Context selection (sources and references) integration
  - ✅ Basic version control and post editing functionality
  - ✅ Post detail/edit page with comprehensive editing capabilities
  - ✅ Version history tracking and management
  - ✅ Context management for adding/removing sources and references
  - ✅ E2E test suite covering complete workflow

### Phase 3: Enhanced Features

- **Task 007: Authorization Flow Refactoring** ✅ - Complete

  - See: `/tasks/007-authorization-middleware.md`
  - ✅ Created three-tier API route authorization middleware (`withAuth`, `withTeamAuth`, `withResourceAuth`)
  - ✅ Standardized error responses across all API endpoints with consistent format
  - ✅ Added comprehensive resource ownership verification for posts, context, prompts, and versions
  - ✅ Migrated 12 API routes to use centralized middleware, eliminating ~200 lines of repetitive code
  - ✅ Maintained backward compatibility with 81% E2E test success rate
  - ✅ Enhanced security with type-safe implementation and proper session handling

- **Task 008: Admin User Management** ✅ - Complete

  - See: `/tasks/008-admin-user-management.md`
  - ✅ Added `isAdmin` boolean column to users table with migration
  - ✅ Created admin authentication middleware (`withAdminAuth`)
  - ✅ Built admin UI components (`AdminOnly` wrapper, `useIsAdmin` hook)
  - ✅ Implemented admin navigation and basic admin page structure
  - ✅ E2E testing for admin access functionality

- **Task 009: System Prompts Management** ✅ - Complete

  - See: `/tasks/009-system-prompts-management.md`
  - ✅ System prompts table with admin and user access control
  - ✅ Global system prompt availability across teams
  - ✅ System prompt selection in post creation flow
  - ✅ Admin UI for system prompt CRUD operations
  - ✅ User UI for creating and managing personal system prompts
  - ✅ Post creation integration with customizable system prompts

- **Task 010: AI Generation Logging** ✅ - Complete

  - See: `/tasks/010-ai-generation-logging.md`
  - ✅ Generation logs table for debugging and troubleshooting
  - ✅ Log all AI generation requests and responses
  - ✅ Include user context, metadata, and performance metrics
  - ✅ Admin UI for viewing and analyzing generation logs

- **Task 011: Model Selection and Tracking** ✅ - Complete

  - See: `/tasks/011-model-selection-tracking.md`
  - ✅ Database schema updates with model, provider, and userPrompt fields in post_versions table
  - ✅ Model selection dropdown in post creation form with provider grouping
  - ✅ Track which model was used for each post generation
  - ✅ Store model information in post versions and generation logs
  - ✅ Support multiple AI providers (OpenAI, Anthropic, Google)
  - ✅ Model information display throughout UI (post details, version history, post cards)
  - ✅ Model validation and form requirements
  - ✅ User prompt tracking in version history
  - ✅ Proper model names from llm-info package

- **Task 012: Post Editor UI Adjustments** ✅ - Complete

  - See: `/tasks/012-post-editor-ui-adjustments.md`
  - ✅ Removed the extra info column on the right side from the post editor
  - ✅ Added concise info bar (versions, context) above the editor in one row
  - ✅ Implemented navigation to previous and future versions of the post
  - ✅ Removed the post content preview at the bottom of the post editor
  - ✅ Added user prompt display at the bottom as read-only reference
  - ✅ Created reusable components: VersionNavigation, PostInfoBar, UserPromptDisplay
  - ✅ Improved database architecture by moving initial user prompt to posts table
  - ✅ Enhanced UI with inline editing for title and status via EditableTitle and EditableStatusBadge
  - ✅ Comprehensive E2E testing with 21/21 tests passing

- **Task 013: Multi-Model Post Generation** ✅ - Complete

  - See: `/tasks/013-multi-model-post-generation.md`
  - ✅ Multi-model selection for initial post generation
  - ✅ Concurrent AI generation with real-time progress updates
  - ✅ Version ordering based on AI response completion time
  - ✅ Immediate redirect to post page with live generation tracking
  - ✅ Progress polling with SWR for real-time status updates
  - ✅ Enhanced user experience with multiple model perspectives
  - ✅ Generation jobs tracking with database schema updates
  - ✅ Multi-model selector UI with provider grouping
  - ✅ Comprehensive E2E testing for multi-model workflow

- **Task 014: AI Post Editing Commands (Simplified)** ✅ - Complete

  - See: `/tasks/014-ai-post-editing-commands.md`
  - 4 essential hardcoded editing commands: improve, shorten, expand, humanize
  - Command execution creates new post versions (using existing version system)
  - Simple command buttons in post editor UI
  - Basic diff view to compare edited version with previous version
  - Command tracking in existing post_versions table
  - Global editing commands only (no paragraph-level editing initially)
  - Reuse existing AI service infrastructure with minimal schema update (baseVersionId field)
  - Accurate diff comparison regardless of version order

- **Task 015: User Default Model Settings** ✅ - Complete

  - See: `/tasks/015-user-default-model-settings.md`
  - ✅ Add default model preferences to user profile
  - ✅ User settings page with model selection dropdown
  - ✅ Store default model in users table (defaultModel field)
  - ✅ Pre-select user's default model in post creation and editing forms
  - ✅ Model preference persistence across sessions
  - ✅ Fallback to system default if user preference not set

- **Task 016: Side-by-Side Version Comparison** ✅ - Complete

  - See: `/tasks/016-side-by-side-version-comparison.md`
  - ✅ Side-by-side version comparison UI
  - ✅ Version selector dropdown for choosing comparison versions
  - ✅ Optional diff highlighting toggle

- **Task 017: Version Notes and Scoring** ✅ - Complete

  - See: `/tasks/017-version-notes-scoring.md`
  - ✅ Add personal notes field to post versions
  - ✅ Implement 0-10 scoring system for version quality rating with decimal support
  - ✅ Update version UI to display notes and scores across all views
  - ✅ Version comparison with notes and scores side-by-side editing
  - ✅ Database schema updates for notes and score fields
  - ✅ Compact notes/score editor component with manual save functionality

- **Task 018: Post Export and Import** ✅ - Complete

  - See: `/tasks/018-post-export-import.md`
  - ✅ Allow user to export single post data as comprehensive JSON file
  - ✅ The JSON file contains all post data including title, content, context, versions, generation logs, etc.
  - ✅ Allow user to import JSON file as post with complete data integrity
  - ✅ UUID conflict detection prevents importing posts that already exist
  - ✅ Comprehensive validation and error handling during import process
  - ✅ User-friendly UI with drag-and-drop file upload and progress tracking
  - ✅ Atomic database transactions ensure data consistency

- **Task 019: Ad-Hoc Custom Edit Commands** ✅ - Complete

  - See: `/tasks/019-ad-hoc-custom-edit-commands.md`
  - ✅ Allow users to enter custom AI editing prompts for one-time use
  - ✅ Simple text input field for custom editing instructions with validation
  - ✅ Execute custom commands using existing AI service infrastructure
  - ✅ Track custom commands in post version history
  - ✅ Custom command input component with character limit (500 chars)
  - ✅ API endpoint extended to handle both predefined and custom commands
  - ✅ Editing service updated with function overloads for custom commands
  - ✅ UI integration in post editor with proper loading states and error handling

- **Task 020: AI Post Review Feature** ✅ - Complete

  - See: `/tasks/020-ai-post-review-feature.md`
  - ✅ AI-powered post review functionality in post details page
  - ✅ Hardcoded review prompt for comprehensive feedback generation
  - ✅ Review feedback display as separate section above timeline
  - ✅ Simple review execution button and loading states
  - ✅ Integration with existing AI service infrastructure
  - ✅ Review results stored and displayed in UI

- **Task 021: Multi-Model Editing Commands** ✅ - Complete

  - See: `/tasks/021-multi-model-editing-commands.md`
  - ✅ Replace existing single-model editing with flexible model selection (one or multiple models)
  - ✅ Allow users to select one or more models for editing operations (similar to Task 013 for generation)
  - ✅ Execute editing commands with selected models concurrently and create versions for each
  - ✅ Real-time progress tracking and version creation as each model completes
  - ✅ Reuse existing multi-model infrastructure from post generation
  - ✅ Compare editing results from different models when multiple are selected

- **Task 022: URL Content Fetching Integration** ✅ - Complete

  - See: `/tasks/022-url-content-fetching-integration.md`
  - ✅ Replace basic regex-based URL content extraction with robust url-to-json-markdown library
  - ✅ Enhanced Reddit post and comment parsing with proper metadata extraction
  - ✅ Clean markdown conversion from HTML content for better content quality
  - ✅ Improved source type detection and structured data handling
  - ✅ Content preview and editing capabilities before saving
  - ✅ Backward compatibility with existing URL import functionality

- **Task 023: Allow References to Also Be Sources** ✅ - Complete

  - See: `/tasks/023-references-as-sources.md`
  - ✅ Allow references to function as sources in post creation flow
  - ✅ Remove artificial separation between sources and references
  - ✅ Flexible context role assignment (source, reference, or both)
  - ✅ Smart external link display based on actual usage
  - ✅ Enhanced context selection interface with role indicators
  - ✅ Maintain organizational value while enabling flexible usage

- **Task 024: Payment Gate Implementation** ✅ - Complete

  - See: `/tasks/024-payment-gate-implementation.md`
  - ✅ Implement subscription status checking and enforcement
  - ✅ Block unpaid teams from accessing premium features
  - ✅ User-friendly upgrade prompts with pricing page integration
  - ✅ API-level protection for premium endpoints
  - ✅ Maintain basic functionality for trial users
  - ✅ Subscription status utilities and middleware

- **Task 025: Context Tagging System** - Priority

  - Add basic tagging system for context items (sources and references)
  - Database schema with tags table and many-to-many relationship to context
  - Allow creating tags on-demand when creating or editing context items
  - Tag selection and filtering in post creation context selection
  - Simple tag input with autocomplete for existing tags

- **Advanced Diff Algorithms**

  - Multiple diff granularity options (character, line, sentence level)
  - Configurable diff sensitivity settings
  - Whitespace and case-insensitive diff options
  - Performance optimization for large documents

- **Syntax-Aware Diff Highlighting**

  - Markdown syntax highlighting in diff view
  - Code block syntax highlighting within diffs
  - Preserve formatting and links in diff display
  - Rich text diff visualization

- **Interactive Diff Navigation**

  - Jump to next/previous change controls
  - Change filtering (additions, deletions, modifications)
  - Synchronized scrolling for side-by-side mode
  - Keyboard shortcuts for diff navigation
  - Change statistics and summary dashboard

- **Content Import/Scraping**

  - URL content extraction service
  - Metadata parsing
  - Multiple content type support

- **Advanced Prompt Templates**

  - Template variables and substitution
  - Prompt validation and versioning
  - Conditional logic in prompts
  - Prompt performance analytics

### Phase 4: Polish & Enhancement

- **Advanced Version Control**

  - Detailed version timeline
  - Advanced diff visualization
  - Conflict resolution

- **Advanced Search & Filtering**

  - Global search
  - Advanced filtering
  - Search result highlighting

- **Export Features**
  - Basic format exports (Markdown, HTML)
  - Platform-specific exports
  - Batch export

### Phase 5: Advanced Features

- **Advanced AI Editing Features**

  - Enhanced editing commands with more options (rewrite, formalize, casual, fix-grammar, add-examples, restructure)
  - Paragraph-level editing: users can select specific paragraphs to apply targeted edits
  - Advanced diff visualization before applying changes (side-by-side, interactive)
  - Separate system prompt management for editing commands (different from post creation)
  - Enhanced content extraction: better parsing of AI responses including markdown code blocks
  - Custom editing command creation and templates
  - Command template management and sharing system
  - Command execution history and analytics
  - Database-driven command management system

### Phase 6: Team & Collaboration

- **Archive System**

  - Archive/unarchive posts
  - Archived posts view
  - Permanent deletion

- **Team Collaboration**
  - Team member roles
  - Collaborative editing
  - Comment system
