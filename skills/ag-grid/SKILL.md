---
name: ag-grid-community-angular
description: Implement AG Grid in Angular using only AG Grid Community (MIT). Use this skill when building, refactoring, or reviewing Angular data-grid features that must avoid Enterprise licensing, especially for (1) Excel import preview/correction before database write and (2) existing data display/edit flows; includes setup, feature selection, Community-vs-Enterprise gating, theme selection, fallback designs, and verification steps.
---

# AG Grid Community Angular

## Update test

## Goal

Build Angular data grids with `ag-grid-community` + `ag-grid-angular` only, while preserving spreadsheet-like usability where possible without Enterprise modules.

## Enforce Community-only Boundary

- Install only `ag-grid-angular` (or `ag-grid-angular` + `ag-grid-community`).
- Register only Community modules:
  - safest: `AllCommunityModule`
  - optimized: explicit Community modules only
- Never install/import `ag-grid-enterprise`.
- Never configure Enterprise-only features.
- Run a boundary check before delivery:
  - no `ag-grid-enterprise` in `package.json`, lockfile, or imports
  - no Enterprise-only feature flags in grid options

## Apply Feature Gate

Use this in-file matrix as the source of truth. Do not require external docs to decide feature boundaries.

### Community Capability Matrix (Allowed)

- Core integration: `ag-grid-angular`, `ag-grid-community`, Community modules only.
- Row models: client-side row model, infinite row model.
- Data UX: sorting, basic filtering, pagination, row selection.
- Columns: define/hide/show/resize/move/pin columns, manage column state.
- Rendering: virtualized rendering, custom cell renderer, tooltip, row/cell styles.
- Value pipeline: `valueGetter`, `valueParser`, `valueFormatter`, `valueSetter`.
- Editing: cell editing, basic editors (text/number/date/checkbox/select/large-text), undo/redo.
- Filtering set: text/number/date/bigint filter, quick filter, external filter, floating filters.
- Export/interop: CSV export.
- Accessibility/i18n/theming: keyboard navigation, ARIA, localisation, RTL, theme customization.
- Extension: custom Angular components for editor/renderer/filter/header.
- APIs/events: Grid API + lifecycle/event callbacks.

### Enterprise-only Matrix (Forbidden)

- AI Toolkit
- Sparklines / Integrated Charts
- Set Filter / Multi Filter / Advanced Filter
- Cell Range Selection / Fill Handle / Clipboard Operations
- Formulas / Find
- Advanced Select Editor (Rich Select)
- Batch Editing
- Excel Export
- Aggregation / Row Grouping / Pivoting / Tree Data / Master Detail
- Column Menu / Context Menu / Columns Tool Panel / Filters Tool Panel / Status Bar
- Advanced server-side operations (grouping/pivot/tree/master-detail/transactions)

### Mandatory Fallbacks for Forbidden Requests

- Need Excel export: keep CSV in grid, add backend `.xlsx` export endpoint.
- Need range copy/fill/paste: implement custom paste parser from focused cell and iterate rows/cols.
- Need grouping/pivot/tree/master-detail: aggregate and shape data on backend, render flat rows in Community grid.
- Need enterprise menus/panels/status bar: build Angular toolbar/drawer/popover panels.
- Need formula/find: implement app-level computed fields and search utilities.

## Cover Two Primary Use Scenarios

### Scenario A: Preview and Correct Imported Excel Before Database Write

1. Parse upload data before grid rendering.
- Parse `.xlsx`/`.csv` via backend parser or app parser.
- Convert raw data into typed row objects using target schema.
- Preserve original row index (`sourceRow`) for traceability.

2. Render a validation-first preview grid.
- Show parsed rows in Community grid with editable cells.
- Mark invalid cells with `cellClassRules` and tooltip error messages.
- Add row-level status fields (`valid`, `errorCount`, `errorSummary`).

3. Block invalid submission and allow iterative correction.
- Prevent "import confirm" when required-field/type/range checks fail.
- Keep edits in a changeset over parsed data, not directly in DB.
- Submit only after all blocking errors are resolved.

4. Commit with auditable payload.
- Send cleaned rows + optional rejected-row report to backend.
- Persist import metadata (file name, operator, timestamp, sourceRow).

### Scenario B: Display and Modify Existing Data

1. Load data with concurrency metadata.
- Include `id` and `version`/`updatedAt` fields from backend.
- Keep immutable columns read-only (`editable: false`).

2. Enable efficient browsing and editing.
- Use sorting/filtering/pagination for operator workflows.
- Use client-side model for moderate datasets; infinite model for large datasets.

3. Track and submit delta only.
- Maintain `ChangeSet<rowId, field, newValue, version>`.
- Submit batch patch API instead of full-table overwrite.

4. Handle conflict and recovery.
- On conflict, highlight affected cells/rows and show latest server values.
- Allow user to re-apply or discard local changes.

## Implementation Workflow

1. Confirm requirement-to-feature mapping.
- Map requested behavior to Community capabilities first.
- If request touches Enterprise-only area, propose a Community fallback before coding.

2. Choose data model.
- Use client-side row model for local/medium datasets and rich client interactions.
- Use infinite row model for backend-driven large datasets and lazy loading.
- Push sorting/filtering/pagination to backend when data volume is large.

3. Build Angular baseline.
- Register Community modules at app bootstrap.
- Use `AgGridAngular` in standalone/component imports.
- Define `columnDefs`, `defaultColDef`, `rowData`, and event callbacks.

4. Add Community editing/filtering UX.
- Use basic editors (`text`, `number`, `date`, `checkbox`, `large text`, `select`).
- Use text/number/date/bigint filters + quick filter + external filter.
- Add undo/redo and keyboard navigation where needed.
- Add validation through parser/setter + `cellClassRules`.

5. Add integration concerns.
- Persist row/cell changes with a changeset.
- Use CSV export for outbound data exchange.
- Apply ARIA/localisation/RTL requirements when needed.
- Apply one of the approved built-in themes and brand tokens.

6. Verify boundary and quality.
- Re-scan code for Enterprise APIs/imports.
- Ensure behavior matches fallback designs.
- Document remaining gaps that require Enterprise (if any).
- Validate selected theme for readability and contrast in dense tables.

## Use Angular Baseline Snippet

```ts
import { Component } from '@angular/core';
import { AgGridAngular } from 'ag-grid-angular';
import { AllCommunityModule, ModuleRegistry, type ColDef } from 'ag-grid-community';

ModuleRegistry.registerModules([AllCommunityModule]);

@Component({
  selector: 'app-grid',
  standalone: true,
  imports: [AgGridAngular],
  template: `
    <ag-grid-angular
      style="width: 100%; height: 70vh"
      [columnDefs]="columnDefs"
      [defaultColDef]="defaultColDef"
      [rowData]="rowData"
      [pagination]="true"
    />
  `,
})
export class GridComponent {
  columnDefs: ColDef[] = [
    { field: 'id', editable: false, sortable: true, filter: 'agNumberColumnFilter' },
    { field: 'name', editable: true, sortable: true, filter: 'agTextColumnFilter' },
    { field: 'createdAt', editable: true, filter: 'agDateColumnFilter' },
  ];

  defaultColDef: ColDef = {
    resizable: true,
    sortable: true,
    filter: true,
  };

  rowData = [];
}
```

## Select Theme Deliberately

Choose one built-in Community theme per product context:

- `ag-theme-quartz`: default choice for new products; clean modern density.
- `ag-theme-alpine`: balanced and familiar; good for general enterprise backoffice.
- `ag-theme-balham`: denser visual style for data-heavy power-user screens.
- `ag-theme-material`: only when the app already follows Material design language.

Apply theme selection rules:

1. Bind theme class at container level and keep it switchable.
2. Customize via CSS variables instead of rewriting core grid CSS.
3. Enforce readable row height and contrast (especially for validation/error states).
4. Keep one theme per page to avoid mixed visual language.

Example switch pattern:

```ts
gridThemeClass = 'ag-theme-quartz';
```

```html
<ag-grid-angular
  [class]="gridThemeClass"
  style="width: 100%; height: 70vh"
  [columnDefs]="columnDefs"
  [rowData]="rowData"
/>
```

## Use Fallback Playbook for Enterprise Requests

- Need Excel export: call backend export endpoint that generates `.xlsx`; keep grid export as CSV.
- Need range fill/copy-paste block: build custom paste parser on focused cell + row/col iteration.
- Need row grouping/pivot: aggregate on backend and return flattened rows.
- Need column/context menu/tool panel: build Angular toolbar + drawer/popover controls.
- Need find/formula: implement app-level search and computed fields in view model.

## Return Output in This Format

- Provide a short plan with requested capability, Community mapping, and fallback (if required).
- Produce Angular code that runs without `ag-grid-enterprise`.
- Include a final boundary checklist result.
