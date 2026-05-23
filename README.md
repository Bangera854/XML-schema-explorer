# XSD Schema Explorer

> A clean, interactive tree view for `.xsd` files — instantly understand complex schemas with click-to-jump navigation, hover tooltips, and constraint visualization.

---

## Features

### 🌳 Interactive Schema Tree
A dedicated **XSD Explorer** panel in the Activity Bar shows the complete logical structure of your schema:

- **Global Elements** — all top-level `xs:element` declarations
- **Complex Types** — all `xs:complexType` definitions with their full hierarchy
- **Simple Types** — `xs:simpleType` with restriction facets
- **Attribute Groups** — reusable attribute collections
- **Groups** — named model groups

### 🖱️ Click-to-Jump Navigation
Click any node in the tree → VS Code instantly **jumps to the exact line** where that element or type is defined, with a 1.5-second highlight flash so you never lose your place.

### 💬 Rich Hover Tooltips
Hover over any tree node to see:
- Full type information and base type
- `minOccurs` / `maxOccurs` values (displayed as `∞` for `unbounded`)
- All constraint facets: `minLength`, `maxLength`, `pattern`, `enumeration`, `minInclusive`, `totalDigits`, etc.
- Whether the element is `nillable`, `abstract`, or `mixed`
- Documentation from `xs:annotation/xs:documentation`
- Source line number

### ♻️ Live Refresh
- **Auto-refresh on save** — tree updates automatically when you save the XSD file
- **Debounced live refresh** — tree also updates 1.5 seconds after you stop typing
- **Manual refresh** — click the refresh button or run `XSD Schema Explorer: Refresh Tree`

### 📊 Occurrence Indicators
Elements clearly show their cardinality:
- `[0..1]` — optional
- `[0..∞]` — zero or more  
- `[1..∞]` — one or more
- `[2..5]` — custom range
- (no badge) — exactly once (required)

---

## Getting Started

1. **Install** the extension from the VS Code Marketplace
2. **Open** any `.xsd` file
3. Click the **XSD Explorer icon** in the Activity Bar (left sidebar)
4. The **Schema Tree** panel opens with your schema structure

No configuration needed. No Java. No external APIs. 100% local.

---

## Commands

| Command | Description |
|---------|-------------|
| `XSD Schema Explorer: Refresh Tree` | Force-refresh the schema tree |
| `XSD Schema Explorer: Collapse All` | Collapse all nodes |

---

## Configuration

| Setting | Default | Description |
|---------|---------|-------------|
| `xsdSchemaExplorer.autoRefresh` | `true` | Auto-refresh tree on file save |
| `xsdSchemaExplorer.showOccurrenceIndicators` | `true` | Show `[min..max]` badges |
| `xsdSchemaExplorer.showTypeNames` | `true` | Show type names next to element names |

---

## Supported XSD Constructs

| Construct | Supported |
|-----------|-----------|
| `xs:element` (global & local) | ✅ |
| `xs:complexType` | ✅ |
| `xs:simpleType` | ✅ |
| `xs:sequence`, `xs:choice`, `xs:all` | ✅ |
| `xs:attribute` | ✅ |
| `xs:attributeGroup` | ✅ |
| `xs:group` | ✅ |
| `xs:extension` (inheritance) | ✅ |
| `xs:restriction` + all facets | ✅ |
| `xs:annotation` / `xs:documentation` | ✅ |
| `xs:include` / `xs:import` | ✅ (listed) |
| `xs:any` | ✅ |

---

## Tree Icons

| Icon | Meaning |
|------|---------|
| 🔵 Variable | Required element |
| ⚪ Field | Optional element (`minOccurs=0`) |
| 🟠 Class | Complex type |
| 🟢 String | Simple type |
| 🔷 Property | Attribute |
| 📦 Namespace | Attribute group |
| 📐 Module | Group |
| `⟨sequence⟩` | Ordered sequence |
| `⟨choice⟩` | Choice (pick one) |
| `⟨all⟩` | All (any order) |
| `extends X` | Type extension |
| `restricts X` | Type restriction |

---

## Example

Open a large `payment-service.xsd` and instantly see:

```
Schema: payment-service.xsd
├── Global Elements (3)
│   ├── PaymentRequest         [1..1]  PaymentRequestType
│   │   ├── transactionId      [1..1]  xs:string
│   │   ├── amount             [1..1]  xs:decimal
│   │   ├── customer           [0..1]  CustomerType
│   │   │   ├── extends BaseCustomer
│   │   │   ├── id             [1..1]  xs:string
│   │   │   └── address        [0..1]  AddressType
│   │   └── notes              [0..1]  xs:string
│   ├── PaymentResponse        [1..1]  PaymentResponseType
│   └── PaymentError           [1..1]  PaymentErrorType
├── Complex Types (8)
│   ├── PaymentRequestType
│   ├── CustomerType
│   └── ...
└── Simple Types (4)
    ├── CurrencyCode
    └── ...
```

Click `customer` → cursor jumps straight to `<xs:element name="customer"...>`.
Hover `amount` → tooltip shows `minInclusive: 0.01, totalDigits: 10`.

---

## Performance

- Handles schemas with **5000+ lines** without lag
- Debounced live updates prevent excessive re-parsing while typing
- Zero external dependencies — pure TypeScript, runs entirely in VS Code

---

## Why XSD Schema Explorer?

| | XSD Treeview | Red Hat XML | **XSD Schema Explorer** |
|--|--|--|--|
| Dedicated tree view | Basic | ❌ | ✅ Full |
| Click-to-jump | ❌ | ❌ | ✅ |
| Hover constraints | ❌ | Partial | ✅ All facets |
| Occurrence indicators | ❌ | ❌ | ✅ |
| Live auto-refresh | ❌ | ❌ | ✅ |
| Zero dependencies | ✅ | ❌ (Java) | ✅ |

---

*****v1.2.2 - Older version***** 
🔍  **Live search** – real‑time filtering with `Ctrl+F`, match badges, and auto‑expansion.

### Added Update 1.2.3
- **Cross‑file resolution** – `xs:include` and `xs:import` are now resolved recursively. Click‑to‑jump works across multiple files.
- **Live search / filter** – Press `Ctrl+F` to filter the tree by name, type, or attribute (added in v1.2.2, now fully integrated).


## 🗺️ Roadmap / Upcoming Features

The following features are planned for future releases:

- **Graphical diagram** – Visual schema overview using Mermaid.
- **Sample XML generation** – Right‑click any complex type to generate a sample XML instance.
- **Enhanced `xs:any` tooltips** – Display namespace and processContents details.

---



## License

MIT
