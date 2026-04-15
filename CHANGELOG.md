# Changelog

All notable changes to this project will be documented in this file.

## [Unreleased]

### Added
- Function `sleep_tip(hours_slept)` to provide advice based on sleep duration
- Function `stress_tip(level)` to give stress management tips
- Input validation for sleep hours using try/except
- Input validation for stress level with range checking (0–2)
- User-friendly prompts and messages
- Simple command-line interface for interaction

### Changed
- Improved clarity of user prompts for better usability
- Organized code into separate functions for readability and reuse

### Fixed
- Prevented crashes from invalid numeric input using exception handling
- Ensured stress level input stays within valid range

---

## [1.0.0] - 2026-02-28

### Added
- Initial release of Mini Stress-Helper program
- Sleep tracking and feedback system
- Stress level evaluation with tips
- Basic error handling for user inputs
