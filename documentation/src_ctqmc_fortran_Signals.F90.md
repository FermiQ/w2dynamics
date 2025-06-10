# Overview

This file src/ctqmc_fortran/Signals.F90 contains...
This Fortran module, `signals`, provides a portable way to handle UNIX signals within a Fortran 90 program. It defines constants for common signal numbers (like `SIGINT`, `SIGUSR1`, `SIGTERM`) and allows registering custom signal handlers or using predefined ones.

# Key Components

- **MODULE signals:** [Requires manual description]
  - **PARAMETER SIGNAL_INT, SIGNAL_USR1, etc.:** [Requires manual description] (Integer parameters representing standard UNIX signal numbers.)
  - **PARAMETER HANDLER_DFL, HANDLER_ERR:** [Requires manual description] (Constants for specifying default signal handling or indicating an error.)
  - **VARIABLE any_signal_fired (volatile logical):** [Requires manual description] (Set to `.TRUE.` if any trapped signal occurs.)
  - **VARIABLE signals_fired (volatile logical array):** [Requires manual description] (Array where `signals_fired(signum)` is `.TRUE.` if signal `signum` has occurred.)
  - **VARIABLE last_signal (volatile integer):** [Requires manual description] (Stores the number of the last signal caught.)
  - **VARIABLE write_stderr (volatile logical):** [Requires manual description] (Controls whether `trap_notify` writes a message to stderr. Default is `.TRUE.`.)
  - **VARIABLE repeat_aborts (logical):** [Requires manual description] (If `.TRUE.`, the program will stop if a trapped signal is caught a second time. Default is `.TRUE.`.)
  - **SUBROUTINE register_trap:** [Requires manual description] (Registers a user-provided function (`trap`) as a handler for a given signal number (`sig_num`). It uses conditional compilation for Intel (`iflport`) and GNU/other compilers to call the appropriate underlying `signal` system call.)
  - **SUBROUTINE clear_trap:** [Requires manual description] (Resets the signal handler for a given signal number to its default action.)
  - **FUNCTION signal_number:** [Requires manual description] (Recursive function to correctly extract the signal number passed to a handler, working around a potential GCC bug.)
  - **FUNCTION trap_stop:** [Requires manual description] (A predefined signal handler that prints a message and calls `abort()` to terminate the program.)
  - **FUNCTION trap_notify:** [Requires manual description] (A predefined signal handler that updates the module's `volatile` variables (`any_signal_fired`, `signals_fired`, `last_signal`) to record that a signal was caught. It can optionally print a message to stderr.)
  - **SUBROUTINE reset_notify:** [Requires manual description] (Resets the `volatile` signal tracking variables to their initial states.)
- **PROGRAM signals_test:** [Requires manual description] (A test program included if `Signals_Test` is defined. It registers `trap_notify` for `SIGINT` and `SIGUSR1`, then enters a loop, printing a dot and sleeping, allowing the user to send signals and observe the trapping mechanism.)
  - **INTERFACE sleep:** [Requires manual description] (Interface to C's `sleep` function for the test program.)

# Important Variables/Constants

- The `SIGNAL_*` parameters are important for users of this module to specify which signal to handle.
- The `volatile` logical flags (`any_signal_fired`, `signals_fired`) and `last_signal` are the primary way for the main program to become aware that a signal handled by `trap_notify` has occurred.
[Requires manual identification and description of important variables/constants/common blocks]

# Usage Examples

[Requires manual addition of usage examples if applicable]
```fortran
USE signals
IMPLICIT NONE

CALL register_trap(SIGNAL_INT, trap_notify) ! Register trap_notify for Ctrl+C
! ... main computation loop ...
IF (any_signal_fired) THEN
    WRITE(*,*) "Signal caught! Last signal was: ", last_signal
    IF (signals_fired(SIGNAL_INT)) THEN
        WRITE(*,*) "Ctrl+C was pressed. Cleaning up..."
        ! Perform cleanup
        CALL clear_trap(SIGNAL_INT) ! Optional: reset handler
        CALL reset_notify()         ! Reset flags
        STOP "Program terminated by user."
    END IF
    CALL reset_notify() ! Reset for next potential signal
END IF
! ...
```

# Dependencies and Interactions

- **USE iso_c_binding:** Used for C interoperability, especially for interfacing with the `signal` system call and defining integer kinds.
- **USE iflport:** (Conditional, if `__INTEL_COMPILER` is defined) Used for Intel Fortran specific signal handling.
- Interacts with the operating system's signal handling mechanism via the `signal()` system call (or equivalent).
[Requires manual description of further interactions]
