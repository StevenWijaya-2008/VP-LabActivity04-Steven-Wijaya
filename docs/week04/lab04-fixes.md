# Lab 04 - Fix Log

> Dokumentasi perbaikan tata letak dan responsivitas untuk **Warung Digital (MenuScreen)**.

| Widget | Error / Symptom | Rule broken | Fix |
| :--- | :--- | :--- | :--- |
| **StoreHeader** | `Row` overflowed on the right at 320 dp (54px overflow in `flutter test`) | `Row` gave store title & rating `Text` unbounded horizontal width | Wrapped store title `Column` in `Expanded` and rating `Text` in `Flexible` + `maxLines: 1` + `ellipsis`. |
| **CategoryBar** | `Row` overflowed on the right | Parent (`Row`) forced horizontal layout without scroll constraints | Wrapped `Row` in `SingleChildScrollView(scrollDirection: Axis.horizontal)`. |
| **PromoStrip** | `Row` overflowed on the right at 320 dp | `Row` gave cards unbounded horizontal width | Wrapped `Row` in `SingleChildScrollView(scrollDirection: Axis.horizontal)`. |
| **MenuScreen** | `Column` bottom overflow on landscape/keyboard | Fixed widgets in `Column` exceeded available height (no scrolling) | Replaced `Column` with `CustomScrollView` and converted sections into `Slivers`. |
| **MenuScreen (Zero)**| `RangeError` (crash) on empty list / No empty state | Code assumed `promos[0]` exists (rule: parent relies on unsafe child data) | Added array check `if (promos.length >= 2)`, created `SliverFillRemaining` containing `Key('empty-state')`. |
| **MenuScreen (500)**| App freezes / Render issues on 500 items | `ListView` built everything up front (ignoring lazy rule) | Replaced `ListView` and `GridView.count` with `.builder` variants (`SliverList` / `SliverGrid`). |
| **MenuTile** | `Row` overflowed on the right with 200-char name | `Row` gave a `Text` unbounded width | Wrapped `Column` in `Expanded`, replaced `Spacer` with `SizedBox`, added `maxLines: 2` + `ellipsis`. |
| **PromoCard / MenuCard** | Bottom overflow with 200-char name | `Text` expanded vertically breaking Card limits | Added `maxLines: 2` + `overflow: TextOverflow.ellipsis` to item names. |
| **CartBar** | Tombol di bawah gesture bar / Teks nabrak tombol | Content lacked `SafeArea` / `Row` gave `Text` unbounded width | Wrapped `CartBar` in `SafeArea`, wrapped `Text` in `Expanded` + `maxLines: 1`. |