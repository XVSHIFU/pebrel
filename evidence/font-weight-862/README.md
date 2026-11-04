# Font weight acceptance evidence

Source: XVSHIFU/pebrel commit b0c884648ea6dd2a34a1d0d86ec774b8ed0fe8b1 (issue Kuddev/pebrel#862).

Captured from the real GPUI native test application on Linux with Xvfb and software Vulkan. These are functional/layout captures, not performance measurements. No user's terminal session or configuration was used.

- English/Nord and Chinese/Silver light: 1100 × 900 logical pixels, scale 1.
- English narrow: 800 × 900 logical pixels, scale 1.
- Chinese high DPI: 1100 × 900 logical pixels, scale 1.5.
- Terminal comparison: identical synthetic VT text on a light background, font size 14, regular weights 400 and 700, Liberation Mono and explicit Noto Sans CJK SC. Both families have installed Regular/Bold faces. Existing CJK regular-for-bold behavior remains enabled.

All six ignored native fixture runs completed successfully. Settings captures exercise native_font_weight_menu; terminal captures reuse native_character_grid_preserves_art_text_and_viewport. The settings fixture verifies its selected value, visible bounds and keyboard menu focus. The terminal fixture asserts the viewport/grid and font metrics.

The bundled Maple face alone has only Regular on this Linux setup; its 400/700 output was unchanged. This is an existing backend face-availability limit and is disclosed in the setting hint and PR, not represented as a successful thickness change. The setting does not add synthetic emboldening or font assets.

The application test binary was built with Rust 1.97.1, default features plus gpui-shell,gpui-test-support. CARGO_BUILD_JOBS=1, CARGO_INCREMENTAL=0, profile.test.package.nebula.debug=0 and profile.test.package.nebula.codegen-units=256 reduced build memory; manifests, dependencies and test coverage were not changed.
