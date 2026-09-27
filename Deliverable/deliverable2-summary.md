# Deliverable 2 Summary

## What was completed

Deliverable 2 evaluated the SQE Task Manager project using static analysis and manual code review. The complete repository was reviewed, including the application entry point, configuration, models, database layer, utilities, views, and tests.

## Main findings

- The baseline Pylint score was **6.44/10.00**.
- Major issues included broad exception handling, unused imports and variables, naming and documentation problems, long lines, complexity, and possible maintainability risks.
- Manual review identified additional design concerns that linting alone would not fully detect:
  - Import code mutated caller-provided data.
  - GUI filtering combined database access, filtering, widget updates, and status reporting.
  - Export/import logic contained duplicated error-handling patterns.
  - Database restore could overwrite the live database without sufficient validation.
  - GUI startup was difficult to test because it created the Tk root directly.

## Improvements made

- Narrowed broad exception handling in `utils/data_export.py`.
- Added consistent `DataTransferError` handling for expected data-transfer failures.
- Prevented JSON import from mutating the original decoded records.
- Narrowed startup exception handling in `main.py` to expected Tk and operating-system failures.
- Added and documented project-specific Pylint configuration decisions.
- Recorded verification evidence and limitations.

## Results

Using the project-specific configuration, the reconstructed baseline scored **7.30/10.00** with **281 findings**, while the improved project scored **9.86/10.00** with **15 findings**. The original Deliverable 1 score of **6.44/10.00** improved to **9.86/10.00**, a gain of **3.42 points**.

The existing regression suite contained **18 tests**, all of which passed in the recorded baseline verification. GUI startup was not executed because it requires a desktop display.

## Conclusion

Static analysis substantially improved consistency and exposed several reliability risks, but it was supplemented with manual review because a high Pylint score does not prove correctness or good architecture. The remaining recommendations include extracting pure filtering logic, validating backups before restore, making restore operations atomic, and improving testability of application startup.


