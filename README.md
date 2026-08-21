# Kanban Board

React task board with four workflow columns, per-task detail pages and
persistence to `localStorage`.

*Educational project (2023). Kept public as part of my learning trajectory —
this was the project where component decomposition and lifted state finally
made sense to me.*

## Problem

Build a working Kanban board from a Figma spec: tasks move through four stages,
each task has its own page, and nothing should be lost when the page reloads.

## Solution

A React SPA where all task state lives in one place at the top of the tree and
flows down to the columns. Any change writes through to `localStorage`, so the
board survives a refresh without a backend.

## Key features

- **Four workflow columns** — Backlog, Ready, In Progress, Finished — with tasks
  moving between them.
- **Per-task pages** — each task has a real URL (`/tasks/:taskId`) via React
  Router, so a task can be linked to and opened directly.
- **Persistence without a backend** — the task list is read from `localStorage` on
  mount and written back through a `useEffect` on every change.
- **Component decomposition** — board, list, task detail, forms, dropdown, header
  and footer are separate modules rather than one large file.

## Architecture

```
App.js                    owns task state, syncs it to localStorage
components/
  main/                   routing: board (/) and task detail (/tasks/:taskId)
  board/                  the four-column layout
  list/                   one column and its task links
  tasks-detail/           single task page
  forms/                  add-new-task form
  dropdown/               status/selection control
  header/ footer/         layout, task counters
```

State is deliberately lifted to `App.js` rather than scattered — the columns are
presentational and receive `tasks` / `setTasks` as props.

## Tech stack

React 18 · React Router 6 · `localStorage` · CSS per component

## How it works

```bash
npm install
npm start      # http://localhost:3000
npm run build
```

## My role

Built the entire application from the Figma spec — component structure, state
model, routing and styling.

## Challenges / lessons

The real lesson here was deciding *where state should live*. My first attempt
kept task data inside individual column components, which made moving a task
between columns awkward. Lifting everything to `App.js` and passing setters down
made the data flow obvious — and made the `localStorage` sync a single
`useEffect` instead of scattered writes.

## Status

Archived — educational project, completed 2023. Not in active development.

---

## Русская версия

**Что это:** доска задач на React с четырьмя колонками рабочего процесса,
отдельными страницами задач и сохранением в `localStorage`.

*Учебный проект (2023). Оставлен публичным как часть траектории обучения —
именно на нём я окончательно понял декомпозицию на компоненты и подъём
состояния.*

**Задача:** собрать рабочую канбан-доску по макету из Figma: задачи проходят
четыре стадии, у каждой задачи своя страница, и ничего не должно теряться при
перезагрузке страницы.

**Решение:** SPA на React, где всё состояние задач живёт в одном месте наверху
дерева и спускается вниз в колонки. Любое изменение записывается в
`localStorage`, поэтому доска переживает обновление страницы без бэкенда.

**Ключевое:**

- **Четыре колонки** — Backlog, Ready, In Progress, Finished — с перемещением
  задач между ними.
- **Страницы задач** — у каждой задачи настоящий URL (`/tasks/:taskId`) через
  React Router, на задачу можно дать ссылку и открыть напрямую.
- **Сохранение без бэкенда** — список задач читается из `localStorage` при
  монтировании и записывается обратно через `useEffect` при каждом изменении.
- **Декомпозиция на компоненты** — доска, колонка, детальная страница задачи,
  формы, дропдаун, шапка и футер вынесены в отдельные модули, а не свалены в
  один файл.

**Стек:** React 18 · React Router 6 · `localStorage` · CSS на компонент.

**Запуск:** `npm install` → `npm start` (http://localhost:3000).

**Моя роль:** всё приложение по макету Figma — структура компонентов, модель
состояния, роутинг и стили.

**Что было сложным:** главный урок здесь — понять, *где должно жить состояние*.
В первой версии данные задач лежали внутри самих колонок, из-за чего перенос
задачи между колонками получался неуклюжим. Подъём всего состояния в `App.js`
и передача сеттеров вниз сделали поток данных очевидным — и превратили
синхронизацию с `localStorage` в один `useEffect` вместо разбросанных записей.

**Статус:** архив — учебный проект, завершён в 2023, не развивается.
