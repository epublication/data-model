# ePublication API Documentation

Developer documentation for the ePublication (Swiss Official Gazettes
Portal) external API.

## Contents

- [Authentication](docs/authentication.md) — credential types, header format,
  key issuance; single source of truth for auth across all documents below.
- [Announcement Export](docs/announcement-export.md) — for public consumers and
  authenticated third-party applications that search and retrieve
  published announcements.
- [Announcement Import](docs/announcement-import.md) — for developers of
  upstream systems (Fachapplikationen) that generate announcements and
  submit them for publication.
- [Migration Guide: SHAB → ePublication](docs/migration-shab.md) — mapping of
  legacy SHAB (Schweizerisches Handelsamtsblatt) announcement codes to the
  new ePublication announcement types.

## Status

This documentation is under active development. Sections marked `TODO`
are open items pending confirmation and should not be treated as final.
See individual documents for details.
