# Task 012: Post Editor UI Adjustments

## Progress Summary

**Status**: Not Started

- [ ] Step 1: Create Version Navigation Component
- [ ] Step 2: Create Compact Info Bar Component
- [ ] Step 3: Create User Prompt Display Component
- [ ] Step 4: Implement Version Navigation Logic
- [ ] Step 5: Refactor Post Detail Page Layout
- [ ] Step 6: Update PostEditor Component
- [ ] Step 7: Testing and Polish

## Overview

Refactor the post editor UI to be more concise and user-friendly by:

- Removing the extra info column on the right side from the post editor
- Putting concise info (versions, context) above the editor in one row
- Adding navigation to previous and future versions of the post
- Removing the post content preview at the bottom of the post editor
- Showing the user prompt at the bottom of the post editor as read-only reference

## Current State Analysis

### Current Layout Structure

The post detail page (`/dashboard/posts/[id]/page.tsx`) currently uses a 3-column grid layout:

- **Main Content (2/3 width)**: PostEditor component + Current Content Preview card
- **Sidebar (1/3 width)**: VersionHistory + PostContextManager + Post Information cards

### Current Components

- `PostEditor` - Main editing interface with title, content, status, and change summary
- `VersionHistory` - Sidebar component showing all versions with selection capability
- `PostContextManager` - Sidebar component for managing sources and references
- `Current Content Preview` - Card showing the current version content below the editor

## Target State

### New Layout Structure

- **Header**: Post title, metadata, and status (unchanged)
- **Info Bar**: Concise version info, context counts, and version navigation in one row
- **Main Editor**: Full-width PostEditor component (no sidebar)
- **User Prompt Reference**: Read-only display of the user prompt at the bottom

### UI Improvements

1. **Consolidated Info Bar**: Display version count, context counts, and navigation controls
2. **Version Navigation**: Previous/Next buttons to navigate between versions
3. **Simplified Layout**: Remove sidebar, make editor full-width
4. **User Prompt Display**: Show the current version's user prompt as reference

## Implementation Steps

### Step 1: Create Version Navigation Component

Create a new `VersionNavigation` component that provides:

- Current version indicator (e.g., "Version 3 of 5")
- Previous/Next navigation buttons
- Version selection dropdown for quick access
- Compact design suitable for horizontal layout

**Files to create/modify:**

- `components/posts/version-navigation.tsx` - New component
- `components/posts/index.ts` - Export new component

### Step 2: Create Compact Info Bar Component

Create a new `PostInfoBar` component that displays:

- Version navigation (using VersionNavigation component)
- Context counts (X sources, Y references)
- Quick access to context management
- Model information for current version

**Files to create/modify:**

- `components/posts/post-info-bar.tsx` - New component
- `components/posts/index.ts` - Export new component

### Step 3: Create User Prompt Display Component

Create a new `UserPromptDisplay` component that shows:

- Current version's user prompt in a read-only format
- Collapsible/expandable design to save space
- Clear labeling and styling for reference context

**Files to create/modify:**

- `components/posts/user-prompt-display.tsx` - New component
- `components/posts/index.ts` - Export new component

### Step 4: Implement Version Navigation Logic

Add version navigation functionality to the post detail page:

- Track current version index in component state
- Implement previous/next navigation handlers
- Update PostEditor to show selected version content
- Handle version switching with proper data loading

**Files to modify:**

- `app/(dashboard)/dashboard/posts/[id]/page.tsx` - Add version navigation state and handlers

### Step 5: Refactor Post Detail Page Layout

Update the post detail page to use the new layout:

- Remove the 3-column grid layout
- Add the PostInfoBar above the editor
- Make PostEditor full-width
- Remove the Current Content Preview card
- Add UserPromptDisplay at the bottom
- Update responsive design for mobile

**Files to modify:**

- `app/(dashboard)/dashboard/posts/[id]/page.tsx` - Complete layout refactor

### Step 6: Update PostEditor Component

Modify the PostEditor to work better in the new layout:

- Ensure proper full-width styling
- Optimize for the new single-column layout
- Maintain all existing functionality

**Files to modify:**

- `components/posts/post-editor.tsx` - Layout and styling updates

### Step 7: Testing and Polish

- Test version navigation functionality
- Verify responsive design on different screen sizes
- Ensure all existing functionality still works
- Update any broken tests
- Polish styling and user experience

**Files to test/modify:**

- E2E tests for post editing workflow
- Component styling and responsive behavior

## Acceptance Criteria

### Functional Requirements

- [ ] Version navigation works correctly (previous/next buttons)
- [ ] Version selection dropdown shows all versions
- [ ] Context information is displayed compactly above editor
- [ ] User prompt is shown at bottom as read-only reference
- [ ] All existing post editing functionality is preserved
- [ ] Version switching updates editor content correctly

### UI/UX Requirements

- [ ] Layout is more compact and user-friendly
- [ ] No sidebar on the right side of the editor
- [ ] Info bar displays version and context information in one row
- [ ] Editor takes full width of the available space
- [ ] User prompt display is collapsible/expandable
- [ ] Responsive design works on mobile devices

### Technical Requirements

- [ ] No breaking changes to existing API endpoints
- [ ] Component reusability maintained
- [ ] TypeScript types properly defined
- [ ] Existing tests pass or are updated accordingly
- [ ] Performance is not degraded

## Files Involved

### New Files

- `components/posts/version-navigation.tsx`
- `components/posts/post-info-bar.tsx`
- `components/posts/user-prompt-display.tsx`

### Modified Files

- `app/(dashboard)/dashboard/posts/[id]/page.tsx`
- `components/posts/post-editor.tsx`
- `components/posts/index.ts`

### Potentially Affected Files

- E2E tests related to post editing
- Any components that depend on the current layout

## Notes

- Maintain backward compatibility with existing data structures
- Ensure the new layout works well on both desktop and mobile
- Consider accessibility implications of the new navigation controls
- The version navigation should be intuitive and not overwhelming
- User prompt display should be helpful but not intrusive

## Dependencies

- Existing post detail API endpoints
- Current PostEditor component functionality
- Version history data structure
- Context management system
