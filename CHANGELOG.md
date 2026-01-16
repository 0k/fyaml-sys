# Changelog

All notable changes to this project will be documented in this file.

## [0.2.7+fy0.9.3] - 2026-01-16

### Changed

- Updated libfyaml submodule from v0.9 to v0.9.3

### Fixed

- Added `libc::iovec` import to support new `sys/uio.h` dependency in
  libfyaml v0.9.3

### Upstream libfyaml changes (v0.9 to v0.9.3)

#### New Public API

- `fy_shutdown()` - Cleanup function for proper resource release at exit
- `fy_event_get_type()` - Simple wrapper to get event type
- `fy_parser_parse_peek()` - Peek at next event without consuming
- `fy_parser_skip()` - Skip the next event
- `fy_parser_count_sequence_items()` - Count items in a sequence
- `fy_parser_count_mapping_items()` - Count items in a mapping
- `fy_parser_get_mode()` - Get current parser mode (YAML/JSON)
- `fy_emit_body_node()` - Emit a node body
- `fy_node_delete()` - Delete a node from document
- `fy_node_get_tag0()` - Get null-terminated tag string
- `fy_node_get_tag_length()` - Get tag length
- `fy_event_report()` / `fy_event_vreport()` - Event-based error reporting
- `fy_diag_set_error()` - Set diagnostic error state
- `fy_diag_event_report()` / `fy_diag_event_vreport()` - Diagnostic event reporting

##### Composer API (new)

- `fy_composer_create()` / `fy_composer_destroy()`
- `fy_composer_process_event()`
- `fy_composer_get_cfg()` / `fy_composer_get_cfg_userdata()`
- `fy_composer_get_diag()`
- `fy_composer_get_path()` / `fy_composer_get_root_path()` / `fy_composer_get_next_path()`

##### Document Builder API (new)

- `fy_document_builder_create()` / `fy_document_builder_destroy()`
- `fy_document_builder_create_on_parser()`
- `fy_document_builder_reset()`
- `fy_document_builder_get_document()`

##### Document Iterator enhancements

- `fy_document_iterator_create_cfg()`
- `fy_document_iterator_create_on_document()`
- `fy_document_iterator_create_on_node()`
- `fy_document_iterator_generate_next()`

##### New Types and Enums

- `struct fy_composer` - Composer state
- `struct fy_composer_cfg` - Composer configuration
- `struct fy_composer_ops` - Composer callbacks
- `struct fy_document_builder` - Document builder state
- `struct fy_document_builder_cfg` - Document builder configuration
- `struct fy_document_iterator_cfg` - Document iterator configuration
- `enum fy_event_part` - Event part selector (VALUE, TAG, ANCHOR)
- `enum fy_parser_mode` - Parser mode (YAML, JSON)
- `enum fy_document_iterator_cfg_flags` - Iterator configuration flags
- `enum fy_path_parse_cfg_flags` - Path parser configuration flags

#### Bug Fixes

- Fixed segmentation fault in `fy_reader_*` functions (issue #133)
- Fixed use-after-free in document acceleration
- Fixed double-free in `fy_node_setup_path_expr_data`
- Fixed infinite loop in scan directive for bad UTF-8 input
- Fixed crash on issue #107
- Fixed memory leaks in walk operations
- Fixed memory leak in composer with back-to-back complex keys
- Fixed broken emit flow mode
- Fixed wrong length return when buffer ends mid-UTF8
- Fixed block scalar end linebreak and whitespace handling

#### Performance Improvements

- Reworked parsing for better performance
- Optimized UTF-8 handling methods
- Optimized token analysis for simple plain scalars
- Optimized output of simple plain scalars
- Thread-safe lockless allocator operations

#### Other Changes

- Allocator infrastructure with multiple allocator types (linear, mremap, dedup, auto)
- Improved CMake support matching autoconf functionality
- Cross-compilation support for both autotools and CMake
- New atomic helpers for thread safety
- Improved portability (NetBSD, GNU/Hurd, macOS fixes)

## [0.2.6+fy0.9.1-alpha-g1f520e6]

- Previous release based on libfyaml v0.9 pre-release

## [0.2.5+fy0.8.0]

- Initial fork maintenance, based on libfyaml v0.8.0
