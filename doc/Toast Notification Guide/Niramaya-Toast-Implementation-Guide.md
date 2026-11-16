# Niramaya Mobile App — Toast Notification Guide

**Purpose:** This guide explains how to use the reusable toast notification system when adding features or screens to the Niramaya React Native / Expo application.

**Toast component location:** `mobile/src/components/toast/`

```text
src/components/toast/
├── Toast.tsx
├── ToastProvider.tsx
├── toast.types.ts
└── useToast.ts
```

## 1. What the toast system is for

Use a toast to give brief, non-blocking feedback after an operation succeeds or fails. The system exposes four notification types:

- `success` — an operation completed successfully.
- `error` — an operation failed.
- `warning` — the user should be aware of a condition or risk.
- `info` — useful neutral information.

The toast system is intended for operation feedback, not as a replacement for form validation, inline error messages, confirmation dialogs, or loading indicators.

## 2. Before using a toast

The `ToastProvider` should be mounted once in the application root layout so screens throughout the app can access the same toast context. In Niramaya, the provider is integrated at the root level.

If a new screen is inside the existing application navigation, you normally do **not** need to add another provider. Just use the hook in the screen component.

## 3. Import and initialise the hook

In the screen where you want to show a toast, import `useToast` and initialise it inside the component:

```tsx
import useToast from "@/components/toast/useToast";

export default function ExampleScreen() {
  const toast = useToast();

  // Existing screen logic and JSX...
}
```

Call the hook at the top level of the component, not inside an event handler, condition, loop, or nested function.

## 4. Available API

### Convenience methods

Use these for the most common cases:

```tsx
// Success
toast.success("Profile Updated", "Your profile has been saved successfully.");

// Error
toast.error("Update Failed", "Unable to save your profile. Please try again.");

// Warning
toast.warning("Unsaved Changes", "You have changes that have not been saved.");

// Information
toast.info("Sync Started", "Your data is being synchronised.");

// Hide the currently displayed toast
toast.hide();
```

The convenience methods accept a title and a message. Keep both concise and specific to the action that just occurred.

### Configurable method

Use `toast.show()` when you need to configure additional toast options:

```tsx
toast.show({
  type: "success", // "success" | "error" | "warning" | "info"
  title: "Changes Saved",
  message: "Your settings have been updated.",
  // Optional configuration:
  duration: 3000,
  position: "top",
  // action: ...
});
```

`duration`, `position`, and `action` are optional configuration fields exposed by the toast API. Check `toast.types.ts` for the exact accepted values and action shape before using non-default options.

## 5. Standard pattern: show feedback after an API operation

Show a success toast only after the awaited operation has completed successfully. Show an error toast in `catch`.

```tsx
const handleSave = async () => {
  try {
    await updateProfile(formData);

    toast.success(
      "Profile Updated",
      "Your personal information has been saved successfully.",
    );
  } catch (err) {
    const errorMessage =
      err instanceof Error ? err.message : "Unable to update your profile.";

    // Keep the screen's existing inline error if it has one.
    setError(errorMessage);

    toast.error("Update Failed", errorMessage);
  }
};
```

Adapt the API call, state setter, and error extraction to the screen's existing implementation. Do not replace established error handling just to add a toast.

## 6. Pattern: manual pull-to-refresh

For a screen with both initial loading and pull-to-refresh, show toast feedback only for the user-initiated refresh. Do not show a toast every time the screen initially loads.

One simple pattern is to pass a flag to the loader:

```tsx
const loadItems = useCallback(
  async (showRefreshToast = false) => {
    try {
      const response = await getItems();
      setItems(response);

      if (showRefreshToast) {
        toast.success("Content Updated", "The latest content has been loaded.");
      }
    } catch (err) {
      const errorMessage =
        err instanceof Error ? err.message : "Unable to refresh the content.";

      setError(errorMessage); // Preserve the existing inline error.

      if (showRefreshToast) {
        toast.error("Refresh Failed", errorMessage);
      }
    }
  },
  [toast],
);

const handleRefresh = () => {
  loadItems(true);
};
```

Call the loader without the flag for initial loading, pagination, or other background requests. If the existing loader has parameters or dependencies, extend it carefully rather than replacing its current behaviour. Include `toast` in a callback dependency array when the callback uses it and the project's lint rules require it.

## 7. Pattern: success followed by navigation

When an operation succeeds and the screen then navigates away, show the toast after the API call succeeds and before navigation:

```tsx
try {
  await createItem(payload);

  toast.success("Item Created", "Your item has been created successfully.");
  router.replace("/destination");
} catch (err) {
  // Handle and display the error here.
}
```

The global provider is important in this situation: it allows the toast to remain mounted when the originating screen unmounts. If a toast still disappears during navigation, verify that the provider is mounted above the route navigator and is not being remounted during the transition.

## 8. Where to place toast calls

| Screen operation                                 | Recommended feedback                                                |
| ------------------------------------------------ | ------------------------------------------------------------------- |
| Create, save, or update succeeds                 | Success toast after the API call                                    |
| Delete succeeds                                  | Success toast after deletion completes                              |
| Status changes (complete, pause, resume, cancel) | Success toast after the server confirms the change                  |
| API operation fails                              | Error toast in `catch`, using the useful error message              |
| User manually refreshes                          | Success or error toast for that refresh only                        |
| Initial screen load                              | Usually no toast; use the existing loading and error UI             |
| Form validation fails                            | Keep the existing inline validation or field error                  |
| Confirmation is required                         | Keep the confirmation dialog; do not toast before the user confirms |
| Search, filter, tab switch, or pagination        | Usually no toast unless the user needs important operation feedback |

## 9. Good practices

1. **Be specific.** Prefer `"Goal Created"` over `"Success"`.
2. **Use plain language.** Explain what happened and, for errors, what the user can do next when possible.
3. **Show feedback after confirmation.** Do not show success before the API request has completed.
4. **Preserve inline errors.** A toast is additional feedback, not a replacement for an error shown beside a form or field.
5. **Avoid duplicate feedback.** If a screen already displays a success modal or another prominent success message, decide whether a toast adds value. Do not show both automatically.
6. **Avoid noisy notifications.** Do not toast for every render, initial load, filter change, or background request.
7. **Use the correct type.** Success for completed actions, error for failures, warning for caution, and info for neutral updates.
8. **Keep messages short.** The title identifies the action; the message gives the useful detail.
9. **Do not swallow errors.** Preserve the screen's existing logging, error state, and recovery behaviour.
10. **Do not add another provider per screen.** Use the app-level provider.

## 10. Common mistakes to avoid

### Showing success before the request finishes

Incorrect:

```tsx
toast.success("Saved", "Your changes have been saved.");
await saveChanges();
```

Correct:

```tsx
await saveChanges();
toast.success("Saved", "Your changes have been saved.");
```

### Toasting validation errors instead of using field feedback

Keep required-field, invalid-input, and other immediate validation messages in the existing form UI. Use a toast for the result of an attempted operation or a failure that needs broader feedback.

### Toasting initial loading failures when the screen already has an error state

Keep the initial-load error state and retry UI. Reserve refresh toasts for an explicit user refresh when that is the established screen pattern.

### Replacing existing error handling

Do not remove `setError`, `setSubmitError`, or similar state updates just because an error toast has been added. Preserve the existing behaviour and add the toast alongside it where appropriate.

## 11. Adding toast support to a new screen — checklist

- [ ] Confirm the screen is rendered under the root `ToastProvider`.
- [ ] Import `useToast` from `@/components/toast/useToast`.
- [ ] Initialise `const toast = useToast();` at the top level of the component.
- [ ] Identify user-triggered operations that need success or failure feedback.
- [ ] Add success toast after the awaited operation succeeds.
- [ ] Add error toast in `catch`, using the existing error-message handling.
- [ ] Preserve inline errors, validation, confirmation dialogs, and loading states.
- [ ] For refresh, show toast feedback only when the user manually refreshes.
- [ ] Avoid duplicate notifications from existing modals or alerts.
- [ ] Add `toast` to relevant hook dependency arrays where required.
- [ ] Test success, failure, refresh, and navigation behaviour on the target screen.

## 12. Reference files

| File                                     | Responsibility                                           |
| ---------------------------------------- | -------------------------------------------------------- |
| `src/components/toast/Toast.tsx`         | Toast presentation component                             |
| `src/components/toast/ToastProvider.tsx` | Shared provider and toast state/context                  |
| `src/components/toast/toast.types.ts`    | Toast types and configuration definitions                |
| `src/components/toast/useToast.ts`       | Hook and methods used by screens                         |
| `src/app/_layout.tsx`                    | Root application layout where the provider is integrated |

**Recommended location for this guide:** `mobile/docs/TOAST_IMPLEMENTATION_GUIDE.md`

When the toast API changes, update this guide and `toast.types.ts` together so future screen implementations use the current method signatures and option types.
