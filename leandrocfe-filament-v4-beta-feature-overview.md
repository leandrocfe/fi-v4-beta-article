## Introduction

Filament v4 Beta is here — and it's packed with powerful new features that give developers more flexibility, improved architecture, and a smoother UI-building experience.

This article walks you through the key updates and how they can improve your workflow in Filament v4.

> You are currently viewing the features for Filament `4.x`, which is currently in `beta` and is not `stable`. Please report any issues you encounter on [GitHub]().

> Looking for the current stable version? Visit the [3.x documentation]().

## Filament v4 now uses Tailwind CSS v4

[Tailwind CSS v4](https://tailwindcss.com) is a major update focused on performance, flexibility, and modern web standards. It features a reworked configuration system, improved customization, and faster builds—making it easier to tailor your design system at scale.
For the latest features and release notes, visit the [Tailwind CSS blog](https://tailwindcss.com/blog).

## Panel Configuration
[...]

## Authentication

### [Multi-factor authentication](../docs/4.x/users/multi-factor-authentication)

[Multi-factor authentication (MFA)](../docs/4.x/users/multi-factor-authentication) in Filament adds an extra security step beyond the default email and password login.

Filament supports two built-in MFA methods:
- [App authentication](../docs/4.x/users/multi-factor-authentication#app-authentication) using a TOTP app like Google Authenticator, Authy, or Microsoft Authenticator apps.
- [Email authentication](../docs/4.x/users/multi-factor-authentication#email-authentication) which sends a one-time code to the user’s email.

## Resources

### [Singular resources](../docs/4.x/resources/singular)

[Singular resources](../docs/4.x/resources/singular) are ideal when you don't need a full table of records—just a single form for managing one item. If the record doesn't exist, it's created when the form is first submitted. If it does, it's loaded automatically on page load and updated when submitted.
This approach works well for pages like a `Homepage` editor, `Settings` screen, or a user `Profile.`

### [Nested resources](../docs/4.x/resources/nesting)

[Relation managers]() and [relation pages]() make it easy to display and manage related records within a resource.
For example, in a `CourseResource`, you might use a relation manager or page to manage the lessons that belong to a course. This lets you create and edit lessons directly from a table using modals.
But if lessons are more complex, modals might not be enough. In that case, you can give lessons their own resource with full-page create and edit views — this is called a [nested resource](../docs/4.x/resources/nesting).

### [Code quality tips](../docs/4.x/resources/code-quality-tips)

To keep your Filament code clean and maintainable:

- Use [schema and table classes](../docs/4.x/resources/code-quality-tips#using-schema-and-table-classes) to separate large `form()` and `table()` definitions into their own files. This helps avoid bloated methods and improves readability.
- Create [dedicated component classes](../docs/4.x/resources/code-quality-tips#using-component-classes) when individual form inputs, table columns, filters, or actions become complex. This keeps each piece of logic focused and reusable.
- Organize components by `type` and `purpose`, such as putting form inputs under `Schemas/Components` and table actions under `Actions`.

## Navigation

### [Sidebar / Topbar](../docs/4.x/navigation/overview#reloading-the-sidebar-and-topbar)

The `Sidebar` and `Topbar` are now Livewire components, allowing them to be updated dynamically.
If you need to refresh them — for example, after a setting or permission change — you can dispatch a [`refresh-sidebar` or `refresh-topbar`](../docs/4.x/navigation/overview#reloading-the-sidebar-and-topbar) browser event to trigger a reload.

## Schemas

[Schemas](../docs/4.x/schemas/overview) form the foundation of Filament's Server-Driven UI approach.
They let you build user interfaces in PHP using structured configuration objects—no need to write `HTML` or `JavaScript` manually.
These schemas define how your UI looks and behaves, representing components such as [forms fields](../docs/4.x/forms/overview), [infolist entries](../docs/4.x/infolists/overview), [layout components](../docs/4.x/schemas/layouts) and [prime components](../docs/4.x/schemas/primes).

Every Filament UI component — whether it's a form field, a description list, or a static element like text or buttons — is configured through a [schema](../docs/4.x/schemas/overview).
Components are modular, nestable, and reusable, making your interfaces consistent and easy to maintain.

A schema is represented by a `Filament\Schemas\Schema` object, and you can pass an `array` of components to it in the `components()` method.

For a full list of available components, see the [Schemas documentation](../docs/4.x/schemas/overview#available-components).

## Forms

### Rich Editor

[Rich Editor](../docs/4.x/forms/rich-editor) is now using [Tiptap](https://tiptap.dev/), a modern, headless, and highly extensible open source editor framework.

Tiptap gives developers full control over the editing experience. Because it's headless, you decide how it looks — [Tiptap](https://tiptap.dev/) handles the logic.

#### Storing content as HTML or JSON

By default, the rich editor stores content as `HTML`. If you would like to store the content as `JSON` instead, you can use the [`json()` method](../docs/4.x/forms/rich-editor#storing-content-as-json).

#### Custom blocks

[Custom blocks](../docs/4.x/forms/rich-editor#using-custom-blocks) are elements that users can drag and drop into the [rich editor](../docs/4.x/forms/rich-editor).
You can define custom blocks that user can insert into the rich editor using the [`customBlocks()` method](../docs/4.x/forms/rich-editor#using-custom-blocks).

#### Merge tags

[Merge tags](../docs/4.x/forms/rich-editor#using-merge-tags) let users insert "placeholders" — like `{{ name }}` or `{{ today }}` — into rich content.
These tags are replaced with dynamic values when the content is rendered, making them useful for things like personalizing messages or displaying dates.

To enable [merge tags](../docs/4.x/forms/rich-editor#using-merge-tags), use the [`mergeTags()` method](../docs/4.x/forms/rich-editor#using-merge-tags) when configuring the editor.

Users can insert tags by typing `{{` to search, or by using the "merge tags" tool in the toolbar, which opens a panel of available tags for easy insertion.

#### Extending the rich editor

You can [extend the Rich Editor](../docs/4.x/forms/rich-editor#extending-the-rich-editor) in Filament by creating custom plugins. These plugins let you add your own [TipTap extensions](https://tiptap.dev/docs/editor/core-concepts/extensions), toolbar buttons, and rendering behavior.

### Slider

The [slider component](../docs/4.x/forms/slider) lets users select one or more numeric values by dragging a handle along a track — ideal for inputs like ranges, ratings, or percentages.

### Code editor

The [code editor component](../docs/4.x/forms/code-editor) lets users write and edit code directly in the interface.
It supports common languages including `HTML`, `CSS`, `JavaScript`, `PHP`, and `JSON`.

### Table repeaters

[Table repeaters](../docs/4.x/forms/repeater#table-repeaters) display [repeater]() items in a table layout using defined `columns`.
You can configure these columns with the `table()` method and `TableColumn` objects, which map to fields in the repeater's schema.

Each column can be customized:
- `hiddenHeaderLabel()` hides the label visually but keeps it accessible.
- `markAsRequired()` adds a red asterisk to indicate required fields.
- `wrapHeader()` enables line-wrapping for long labels.
- `alignment()` sets header alignment (`start`, `center`, or `end`).
- `width()` defines a fixed width for the column.

### Selecting options from a table in a modal
[ModalTableSelect](../docs/4.x/forms/select#selecting-options-from-a-table-in-a-modal)

[...]

### Using JavaScript

#### `hiddenJs()` and `visibleJs()`

You can conditionally `hide` or `show` fields using the [hidden()]() or [visible()]() methods with a PHP callback.
However, this triggers a full schema reload and a network request whenever the reactive field changes — potentially affecting performance.

For better efficiency, use [`hiddenJs()` or `visibleJs()`](../docs/4.x/forms/overview#hiding-a-field-using-javascript) instead. These methods evaluate JavaScript expressions on the client side, allowing you to toggle field visibility instantly without reloading the schema.

#### `JsContent`

You can dynamically set text content — like [labels](../docs/4.x/forms/overview#setting-a-fields-label) or [belowContent](../docs/4.x/forms/overview#adding-extra-content-to-a-field) — using [`JavaScript` by passing a `JsContent` object](../docs/4.x/forms/overview#using-javascript-to-determine-text-content).
This allows methods like `label()` and `Text::make()` to render `HTML` based on field values.

Inside the `JsContent`, you can use `$state` and `$get` to access the current field's state or other fields in the schema, enabling real-time, reactive text updates without server interaction.

#### `afterStateUpdatedJs()`
When you set the state of another field using `$set()` inside an `afterStateUpdated()` function, it modifies the state — but still triggers a network request to reload the schema.

To avoid this, you can use [`afterStateUpdatedJs()`](../docs/4.x/forms/overview#preventing-the-livewire-component-from-rendering-after-a-field-is-updated), which runs a `JavaScript` expression every time the field value changes.

This approach skips the network request entirely and updates fields instantly on the client side.

In this JavaScript context, you can use `$state`, `$get()`, and `$set()` to interact with field states efficiently.

### Fusing fields together into a group
[FusedGroup](../docs/4.x/forms/overview#fusing-fields-together-into-a-group)

[...]

### Extra content in fields

[Adding extra content to a field](../docs/4.x/forms/overview#adding-extra-content-to-a-field)

[...]

### Partial rendering

[Partial rendering](../docs/4.x/forms/overview#field-partial-rendering)

[...]

## Infolists

### Code entry

[Code entry](../docs/4.x/infolists/code-entry)

[...]

## Tables

### Static data

[...]

## Actions

[...]

## Widgets

[...]

## Notifications

### Error notifications

[Error Notifications](../docs/4.x/panel-configuration#configuring-error-notifications)

[...]

## Conclusion

[...]