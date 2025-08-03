# Release Notes

## [2.0.7] - 2025-08-03

### Added
- ✨ **React 19 Support**: Added React 19 to peerDependencies while maintaining full backward compatibility
- 🔧 **TypeScript Improvements**: Updated JSX types for React 19 compatibility

### Changed
- 📦 **Repository Migration**: Updated repository references from `staylor` to `vuer-ai` organization
- 👤 **Maintainer Update**: Updated package author to Ge Yang <ge.ike.yang@gmail.com>
- 🔄 **Dependency Updates**: Upgraded dev dependencies for React 19 compatibility
- 📚 **Documentation Refresh**: Completely rewrote README with clearer examples and modern best practices

### Fixed
- 🐛 **Build System**: Fixed TypeScript compilation issues with React 19
- 🔧 **Type Safety**: Resolved JSX namespace issues in TypeScript strict mode

### Technical Details
- Maintains compatibility with React 16.6+, 17.x, 18.x, and now 19.x
- Updated `@types/react` to `^19.0.0`
- Fixed TypeScript compilation by using `React.JSX.Element` instead of global `JSX.Element`
- Added `skipLibCheck` to TypeScript build configuration

---

## About This Release

This release focuses on future-proofing the library for React 19 while maintaining the rock-solid thread-safety and server-side rendering capabilities that make react-helmet-async essential for production React applications.

### Migration Notes

**From react-helmet-async < 2.0.7:**
- No breaking changes - this is a backward-compatible upgrade
- React 19 projects can now use this library without compatibility issues
- All existing APIs remain unchanged

**React Version Support:**
- ✅ React 16.6+ - Full support
- ✅ React 17.x - Full support  
- ✅ React 18.x - Full support
- ✅ React 19.x - Full support (new!)

### Why React 19 Support Matters

React 19 introduces several improvements for server-side rendering and meta tag management:
- Better hydration behavior
- Improved type safety with strict TypeScript configurations
- Enhanced performance for server-rendered applications

This library ensures you can adopt React 19 without losing the critical thread-safety features needed for production SSR applications.

---

## Previous Releases

### [2.0.6] and earlier
- Thread-safe server-side rendering
- Apollo GraphQL compatibility
- SEO tag prioritization
- Modern React 16+ support
- Drop-in replacement for react-helmet

For detailed history of earlier releases, see the [commit history](https://github.com/vuer-ai/react-helmet-async/commits/main).