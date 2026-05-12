# ng-investment-calculator

An investment calculator built with Angular 18 as a practice project while following Maximilian Schwarzmuller's [The Complete Guide to Angular](https://www.udemy.com/course/the-complete-guide-to-angular-2/) on Udemy.

## What I learned building this

### Standalone components

Unlike the previous task manager project which used NgModules, this app uses standalone components throughout. Each component declares its own `imports` array directly in the `@Component` decorator.

### Signals for state

Signals are Angular's reactive primitive: the same concept as `ref()` in Vue, `createSignal()` in Solid, or `useState()` in React. When a signal's value changes, anything that reads it updates automatically. The syntax is slightly different: reading requires calling it as a function (`this.initialInvestment()`), and writing uses `.set()`. Form field values and the computed results are both signals here, so the results table re-renders whenever the service updates them without any manual change detection.

### Service with signal-based shared state

`InvestmentService` holds a `results` signal and exposes a `calculate()` method. `UserInputComponent` calls `calculate()` on form submit; `InvestmentResultsComponent` reads `results()` via the same service instance. This is the same singleton pattern as before, but now the shared state is a signal instead of a plain array, so the UI updates without any manual change detection.

### The currency pipe

`{{ row.valueEndOfYear | currency }}` formats a raw number as a localized currency string. Pipes are applied in the template with `|` and must be imported into the component's `imports` array (`CurrencyPipe` from `@angular/common`).

### @if with an else branch

```html
@if (!results) {
  <p>Please enter some values...</p>
} @else {
  <table>...</table>
}
```

The new control flow syntax supports `@else` directly, which is cleaner than the old `*ngIf / ng-template` pattern.

## Stack

- Angular 18 (standalone components)
- TypeScript
- Angular Signals
- Angular Forms (template-driven)
- CurrencyPipe
- Bun
