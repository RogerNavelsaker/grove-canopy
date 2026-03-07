# Canopy — V1 Scope

## One-Liner
Git-native prompt management with section-based composition and inheritance — create, version, validate, and emit prompts as plain files for AI agent consumption.

## V1 Definition of Done

- [ ] Prompt CRUD works: `create`, `show`, `list`, `update`, `archive`
- [ ] Inheritance resolution works: `render` merges parent + child sections correctly (up to 5 levels, cycle detection)
- [ ] Versioning works: `update` creates new versions, `history` shows timeline, `diff` compares versions
- [ ] Pinning works: `pin` locks to a version, `unpin` releases
- [ ] Emit pipeline works: `emit <name>`, `emit --all`, `emit --check` (CI staleness check)
- [ ] Emit supports both `.md` and `.ts` (TypeScript module) output formats
- [ ] Frontmatter (YAML metadata) correctly extracted and rendered
- [ ] Named emit targets with tag-based routing work
- [ ] Schema validation works: `schema create`, `schema show`, `schema list`, `schema rule add`, `validate`
- [ ] Import works: `import` converts a `.md` file into a canopy prompt (section splitting, frontmatter extraction)
- [ ] Git integration: `sync` stages and commits `.canopy/` changes
- [ ] Agent integration: `prime` outputs workflow context, `onboard` installs to CLAUDE.md
- [ ] `--json` flag produces structured output on all commands
- [ ] All tests pass (`bun test`)
- [ ] TypeScript strict mode clean (`bun run typecheck`)
- [ ] Linting passes (`bun run lint`)
- [ ] CI pipeline runs lint + typecheck + test on push/PR
- [ ] Published to npm as `@os-eco/canopy-cli`

## Explicitly Out of Scope for V1

- LLM-powered prompt optimization or rewriting
- A/B testing or prompt experimentation framework
- Remote prompt registry or sharing
- Prompt analytics (usage tracking, performance metrics)
- Visual prompt editor or web UI
- Conditional sections (if/else logic in prompts)
- Template variable interpolation (mustache/handlebars-style `{{var}}` substitution)
- Multi-repo prompt federation
- Prompt dependency graph beyond single-level inheritance
- Auto-versioning based on git commits

## Current State

Canopy is effectively V1-complete. All 23 CLI commands are implemented and tested. 257 tests pass with zero failures. Lint and typecheck are both clean. CI is green. All 71 tracked issues are closed. Published to npm at v0.2.2.

The tool handles the full prompt lifecycle: create, compose via inheritance, version, validate against schemas, emit to files, and integrate with agents. The emit pipeline supports both markdown and TypeScript output.

**Estimated completion: ~98%.** Fully functional for its core purpose.

## Open Questions

- Template variable interpolation (`{{var}}`) is explicitly out of scope here, but greenhouse's supervisor prompt needs it (see `greenhouse-04a7`). Should canopy own variable substitution, or should consumers handle it at render time?
- Is the current max inheritance depth of 5 sufficient, or does real-world usage hit this limit?
