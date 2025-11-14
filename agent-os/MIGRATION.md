## Migration Guide — From nested profiles/workflows → flattened commands
- Commands now live in `agent-os/commands/` as single files; workflows folder removed.
- Agents & standards remain modular under `agent-os/agents/` and `agent-os/standards/`.
- Update any internal links and CI paths accordingly.
