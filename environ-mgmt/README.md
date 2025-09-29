Environ Management Tests
------------------------

Tests for items in the "MPI Environmental Management" chapter.

These are being created in the ompi-tests-public repository
to ensure they are easy to access.

Using autotools to detect if we have the MPI-4.1 remove error code
functionality, otherwise skips.

Usage
-----
 - Ensure MPI `mpicc` in `PATH`
 - Run autogen/configure/make to build test

   ```
     cd environ-mgmt/
     ./autogen.sh && ./configure && make
   ```

 - Run test(s)

   ```
     mpirun -np 1 ./src/test_add_del_err_codes
   ```

 - (Fortran) Build/Run
   ```
     ./autogen.sh && ./configure FC=mpifort && make
     mpirun -np 1 ./src/test_add_err_codes_usempi
     mpirun -np 1 ./src/test_add_err_codes_usempif08
   ```

Example Output
--------------

 - On MPI 3.x
    ```
    laptop:$ mpirun -np 1 ./src/test_add_del_err_codes
    TEST: Success creating error class/code/string (last=92, newlast=94)
    ==== Adds done ====
    ==== Remove estring ====
    Warning: MPI_Remove_error_xxx code/class/string NOT available!
    ==== Remove ecode ====
    Warning: MPI_Remove_error_xxx code/class/string NOT available!
    ==== Remove eclass  ====
    Warning: MPI_Remove_error_xxx code/class/string NOT available!
    DONE: Success
    laptop$ echo $?
    0
    laptop$
    ```

 - On MPI 4.1 or later
    ```
    laptop:$ mpirun -np 1 ./src/test_add_del_err_codes
    TEST: Success creating error class/code/string (last=92, newlast=94)
    ==== Adds done ====
    ==== Remove estring ====
    ==== Remove ecode ====
    TEST: Success reomved error code (oldlast=94, newlast=93)
    ==== Remove eclass  ====
    TEST: Success reomved error class (oldlast=93, newlast=92)
    DONE: Success
    laptop$ echo $?
    0
    laptop$
    ```

