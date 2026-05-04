# Sudoku WPF

<img width="1898" height="978" alt="image" src="https://github.com/user-attachments/assets/0e700cb9-e06c-43e3-a9cd-44fa35517bdb" />
<img width="1117" height="678" alt="image" src="https://github.com/user-attachments/assets/d243ff10-60c4-4962-9702-9570dbe9c12b" />



A desktop Sudoku game built with WPF and C#. Generate puzzles, play, save your progress, share boards by code, and customize the experience with multiple themes and sound options.

This project was developed as a 30% Bagrut (Israeli matriculation) software engineering project.

## Features

- **Configurable boards** — play the classic 9×9 grid or any supported size up to 25×25.
- **Puzzle generator** — every game produces a uniquely solvable puzzle.
- **Hints and checks** — limited per game (5 of each by default) to keep things fair.
- **Show solution** — reveal the full solved board at any time.
- **Save and resume** — store games to a local Access database and pick them up later.
- **Puzzle codes** — copy a puzzle to a short text code and import it back to share with others.
- **Six themes** — Light, Dark, Light Blue, Light Brown, Pink, and Red.
- **Sound and music** — relaxing background music plus UI sound effects, all toggleable.
- **In-app instructions** — multi-page tutorial covering the rules and controls.
- **Custom chrome** — minimize / maximize / close controls and a saver-style overlay.

## Tech Stack

| Layer | Technology |
| --- | --- |
| UI | WPF (XAML) |
| Application | C# on .NET 8 (`net8.0-windows`) |
| Data Access | DAL class library on .NET Framework 4.7.2 |
| Database | Microsoft Access (`.accdb`) via `System.Data.OleDb` |

## Project Structure

```
sudoku-wpf-app/
├── Sudoku_WPF.sln              Solution file
├── Sudoku_WPF/                 WPF presentation project (.NET 8)
│   ├── App.xaml(.cs)           Application entry point
│   ├── MainWindow.xaml(.cs)    Main shell with custom chrome
│   ├── Pages/                  Opening, Game, Settings, Saver, Instructions
│   ├── GameClasses/            Board, Cell, Puzzle, Notes, Game, Code
│   ├── Static/                 Constants, GameSettings, Settings, SoundPlayer
│   └── Assets/                 Icons, Images, Music, Sounds, Themes, Styles
└── DAL/                        Data Access Layer (.NET Framework 4.7.2)
    ├── DBHelper.cs             OleDb connection and query helpers
    └── Data/Sudoku_DB1.accdb   Access database (saved games, settings)
```

## Requirements

- Windows 10 or later
- [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0) (for building) or .NET 8 Desktop Runtime (for running)
- .NET Framework 4.7.2 Developer Pack (for the DAL project)
- [Microsoft Access Database Engine 2016 Redistributable](https://www.microsoft.com/download/details.aspx?id=54920) — required by the OLE DB provider used to read `.accdb` files
- Visual Studio 2022 (recommended) with the `.NET desktop development` workload

## Getting Started

1. Clone the repository:
   ```powershell
   git clone https://github.com/Eitan318/sudoku-wpf-app.git
   cd sudoku-wpf-app
   ```
2. Open `Sudoku_WPF.sln` in Visual Studio 2022, or restore from the CLI:
   ```powershell
   dotnet restore Sudoku_WPF.sln
   ```
3. Update the database path in `DAL/DBHelper.cs` so it points to the `Sudoku_DB1.accdb` file shipped under `DAL/Data/` on your machine. The current connection string is hard-coded to a development path and must be adjusted before first run.
4. Build and run:
   ```powershell
   dotnet build Sudoku_WPF.sln -c Release
   dotnet run --project Sudoku_WPF/Sudoku_WPF.csproj
   ```
   Or press `F5` in Visual Studio with `Sudoku_WPF` set as the startup project.

## How to Play

1. From the **Opening** page, choose **New Game** or **Load Game**.
2. In **Settings**, pick board size, theme, and audio preferences.
3. Click a cell and type a number. Use **Notes** mode to pencil in candidates.
4. Use **Hint** to reveal a single correct value, **Check** to validate your current entries, or **Show Solution** to give up and see the answer.
5. Save the game at any time — it will appear in **Load Game** on your next launch.
6. Use **Copy Code** to export the puzzle as text, and **Import Code** to play someone else's board.

## Configuration

Game-wide constants live in `Sudoku_WPF/Static/Constants.cs`:

| Constant | Default | Purpose |
| --- | --- | --- |
| `BoardConstants.DEFAULT_SIDE` | 9 | Default Sudoku grid size |
| `BoardConstants.MAX_SIDE` | 25 | Maximum supported grid size |
| `GameConstants.HINTS` | 5 | Hints available per game |
| `GameConstants.CHECKS` | 5 | Validation checks per game |

Themes are defined as XAML resource dictionaries in `Sudoku_WPF/Assets/Themes/` and swapped at runtime by `ThemeControl.cs`.

## Known Limitations

- The DAL still targets .NET Framework 4.7.2; migrating it to .NET 8 would simplify packaging.
- The OleDb dependency means the app is Windows-only and requires the Access Database Engine to be installed.

## License

This project is released for educational purposes. See the repository for license details, or contact the author before reuse.

## Author

**Eitan Amir** — 10th grade software engineering student.
