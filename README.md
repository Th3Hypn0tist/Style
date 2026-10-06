# Style

Canonical visual contract for WebGUI and WebEngine surfaces.

Style contains no application logic and no domain-specific presentation rules. It consumes the stable presentation contracts defined by WebGUI and WebEngine and implements them with reusable CSS.

## Deployment

```text
Style repository
-> /style/
```

Canonical entry:

```text
/style/style.css
```

## Ownership

```text
WebGUI
  -> .wg-* primitive/component semantics

WebEngine
  -> .we-* application/composition semantics

Style
  -> visual implementation for .wg-* and .we-*
  -> semantic tokens
  -> dark/light themes

Domain
  -> uses the contracts
  -> does not create a parallel design system
```

Theme selection is explicit:

```html
<html data-theme="dark">
<html data-theme="light">
```

If `data-theme` is absent, the current default is dark.

See `Contracts/` for canonical boundaries.


## Contract consumption

Style is a visual implementation layer only.

It may consume:

```text
WebGUI    -> .wg-* semantics and declared generic UI state vocabularies
WebEngine -> .we-* semantics and declared subsystem state vocabularies
```

Style must not invent new shared class meanings or state/status/variant values. If a value such as `data-state="loading"` is not yet owned by an upstream contract, Style does not implement it yet.

Shared state selectors must remain scoped to their owning presentation namespace. For example, WebGUI's `data-disabled` handling is applied only to declared `.wg-*` structures rather than globally to arbitrary host DOM.

Dark and light themes implement the same semantic token names. Theme files change values only; structural selectors remain in the shared WebGUI/WebEngine CSS.
