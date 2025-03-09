```markdown
# Recent Popular Casts Frame Specification

## 1. OVERVIEW

### Core Functionality
- Fetches 10 most popular casts for given user FID using `/farcaster/feed/user/popular` endpoint
- Displays random cast from curated list with engagement metrics (likes/recasts/replies)
- Enables single-tap reply composition with pre-filled context
- Preserves session state for continuity between interactions

### UX Flow
1. Initial load: Display animated loading state
2. Fetch popular casts → Random selection → Render cast card
3. User options: 
   - Refresh (new random cast)
   - View engagement details (expandable section)
   - Compose reply (pre-filled @handle context)
4. Reply flow: Native composer integration with parent cast reference

## 2. TECHNICAL REQUIREMENTS

### Data Handling
- Use Neynar API for cast popularity metrics (`likes_count`, `recasts_count`)
- Cache response for 2 minutes to prevent duplicate fetches
- Store selected cast metadata in Frame state object

### UI System
- Mobile-first responsive grid (1-3 column adaptive layout)
- Dynamic font scaling for cast text (14-18px range)
- Embedded media containers with aspect ratio locking
- Progressive disclosure for metadata/actions

## 3. FRAMES v2 IMPLEMENTATION

### Interactive Elements
- Canvas-based engagement sparkline visualization
- Swipeable card stack interface (touch/pointer events)
- Contextual input field for reply drafting
- Deep link buttons for cast sharing

### State Management
- Serialize current cast selection in frame state
- Track user interaction history in localStorage
- Maintain session-specific view preferences

### SDK Integration
- Use `sdk.actions.ready()` for frame initialization
- Handle `post_redirect` for native composer integration
- Implement `tx` action type for potential future token interactions

## 4. MOBILE CONSIDERATIONS

### Layout
- Vertical stacking for <500px viewports
- Fixed bottom action bar with primary CTAs
- Avoid horizontal scroll traps
- Oversized touch targets (min 48px²)

### Performance
- Lazy-load non-critical metadata
- Compress embedded images via CDN
- Debounce rapid refresh actions
- Prefetch next potential cast

## 5. CONSTRAINTS COMPLIANCE

### Storage
- Session-persisted state only (no cross-device sync)
- Purge cached data after 5 minutes of inactivity
- Use frame metadata for essential persistence

### Scope
- Zero external API dependencies beyond Neynar
- No user authentication requirements
- Ephemeral interactions only (no history storage)
- Reuse existing UI components from template

### Compliance
- Adhere to Farcaster frame content policies
- Filter NSFW content via Neynar API parameters
- Respect user mute/block lists in cast selection
- Follow WCAG 2.1 AA contrast requirements
```