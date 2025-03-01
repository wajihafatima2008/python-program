# python-program++++++++++
Python News
+++++++++++

What's New in Python 3.10.11 final?
===================================

*Release date: 2023-04-04*

Security
--------

- gh-issue-101727: Updated the OpenSSL version used in Windows and macOS
  binary release builds to 1.1.1t to address CVE-2023-0286, CVE-2022-4303,
  and CVE-2022-4303 per `the OpenSSL 2023-02-07 security advisory
  <https://www.openssl.org/news/secadv/20230207.txt>`_.

- gh-issue-101283: :class:`subprocess.Popen` now uses a safer approach to
  find ``cmd.exe`` when launching with ``shell=True``. Patch by Eryk Sun,
  based on a patch by Oleg Iarygin.

Core and Builtins
-----------------

- gh-issue-102416: Do not memoize incorrectly automatically generated loop
  rules in the parser. Patch by Pablo Galindo.

- gh-issue-102356: Fix a bug that caused a crash when deallocating deeply
  nested filter objects. Patch by Marta Gómez Macías.

- gh-issue-102397: Fix segfault from race condition in signal handling
  during garbage collection. Patch by Kumar Aditya.

- gh-issue-102126: Fix deadlock at shutdown when clearing thread states if
  any finalizer tries to acquire the runtime head lock. Patch by Kumar
  Aditya.

- gh-issue-102027: Fix SSE2 and SSE3 detection in ``_blake2`` internal
  module. Patch by Max Bachmann.

- gh-issue-101967: Fix possible segfault in
  ``positional_only_passed_as_keyword`` function, when new list created.

- gh-issue-101765: Fix SystemError / segmentation fault in iter
  ``__reduce__`` when internal access of ``builtins.__dict__`` keys mutates
  the iter object.

Library
-------

- gh-issue-102947: Improve traceback when :func:`dataclasses.fields` is
  called on a non-dataclass. Patch by Alex Waygood

- gh-issue-101979: Fix a bug where parentheses in the ``metavar`` argument
  to :meth:`argparse.ArgumentParser.add_argument` were dropped. Patch by
  Yeojin Kim.

- gh-issue-102179: Fix :func:`os.dup2` error message for negative fds.

- gh-issue-101961: For the binary mode, :func:`fileinput.hookcompressed`
  doesn't set the ``encoding`` value even if the value is ``None``. Patch by
  Gihwan Kim.

- gh-issue-101936: The default value of ``fp`` becomes :class:`io.BytesIO`
  if :exc:`~urllib.error.HTTPError` is initialized without a designated
  ``fp`` parameter. Patch by Long Vo.

- gh-issue-101566: In zipfile, apply fix for extractall on the underlying
  zipfile after being wrapped in ``Path``.

- gh-issue-101997: Upgrade pip wheel bundled with ensurepip (pip 23.0.1)

- gh-issue-101892: Callable iterators no longer raise :class:`SystemError`
  when the callable object exhausts the iterator but forgets to either
  return a sentinel value or raise :class:`StopIteration`.

- gh-issue-97786: Fix potential undefined behaviour in corner cases of
  floating-point-to-time conversions.

- gh-issue-101517: Fixed bug where :mod:`bdb` looks up the source line with
  :mod:`linecache` with a ``lineno=None``, which causes it to fail with an
  unhandled exception.

- gh-issue-101673: Fix a :mod:`pdb` bug where ``ll`` clears the changes to
  local variables.

- gh-issue-96931: Fix incorrect results from
  :meth:`ssl.SSLSocket.shared_ciphers`

- gh-issue-88233: Correctly preserve "extra" fields in ``zipfile``
  regardless of their ordering relative to a zip64 "extra."

- gh-issue-95495: When built against OpenSSL 3.0, the :mod:`ssl` module had
  a bug where it reported unauthenticated EOFs (i.e. without close_notify)
  as a clean TLS-level EOF. It now raises :exc:`~ssl.SSLEOFError`, matching
  the behavior in previous versions of OpenSSL. The
  :attr:`~ssl.SSLContext.options` attribute on :class:`~ssl.SSLContext` also
  no longer includes :data:`~ssl.OP_IGNORE_UNEXPECTED_EOF` by default. This
  option may be set to specify the previous OpenSSL 3.0 behavior.

- gh-issue-94440: Fix a :mod:`concurrent.futures.process` bug where
  ``ProcessPoolExecutor`` shutdown could hang after a future has been
  quickly submitted and canceled.

Documentation
-------------

- gh-issue-103112: Add docstring to :meth:`http.client.HTTPResponse.read` to
  fix ``pydoc`` output.

- gh-issue-85417: Update :mod:`cmath` documentation to clarify behaviour on
  branch cuts.

- gh-issue-97725: Fix :meth:`asyncio.Task.print_stack` description for
  ``file=None``. Patch by Oleg Iarygin.

Tests
-----

- gh-issue-102980: Improve test coverage on :mod:`pdb`.

- gh-issue-102537: Adjust the error handling strategy in
  ``test_zoneinfo.TzPathTest.python_tzpath_context``. Patch by Paul Ganssle.

- gh-issue-101377: Improved test_locale_calendar_formatweekday of calendar.

Build
-----

- gh-issue-102711: Fix ``-Wstrict-prototypes`` compiler warnings.

Windows
-------

- gh-issue-101759: Update Windows installer to SQLite 3.40.1.

- gh-issue-101614: Correctly handle extensions built against debug binaries
  that reference ``python3_d.dll``.

macOS
-----

- gh-issue-103207: Add instructions to the macOS installer welcome display
  on how to workaround the macOS 13 Ventura “The installer encountered an
  error” failure.

- gh-issue-101759: Update macOS installer to SQLite 3.40.1.

- gh-issue-87235: On macOS ``python3 /dev/fd/9 9</path/to/script.py`` failed
  for any script longer than a couple of bytes.


What's New in Python 3.10.10 final?
===================================

*Release date: 2023-02-07*

Core and Builtins
-----------------

- gh-issue-101400: Fix wrong lineno in exception message on
  :keyword:`continue` or :keyword:`break` which are not in a loop. Patch by
  Dong-hee Na.

- gh-issue-101372: Fix :func:`~unicodedata.is_normalized` to properly handle
  the UCD 3.2.0 cases. Patch by Dong-hee Na.

- gh-issue-101046: Fix a possible memory leak in the parser when raising
  :exc:`MemoryError`. Patch by Pablo Galindo

- gh-issue-100942: Fixed segfault in property.getter/setter/deleter that
  occurred when a property subclass overrode the ``__new__`` method to
  return a non-property instance.

- gh-issue-100892: Fix race while iterating over thread states in clearing
  :class:`threading.local`. Patch by Kumar Aditya.

- gh-issue-100776: Fix misleading default value in :func:`input`'s
  ``__text_signature__``.

- gh-issue-100374: Fix incorrect result and delay in :func:`socket.getfqdn`.
  Patch by Dominic Socular.

- gh-issue-100050: Honor existing errors obtained when searching for
  mismatching parentheses in the tokenizer. Patch by Pablo Galindo

- bpo-32782: ``ctypes`` arrays of length 0 now report a correct itemsize
  when a ``memoryview`` is constructed from them, rather than always giving
  a value of 0.

Library
-------

- gh-issue-100795: Avoid potential unexpected ``freeaddrinfo`` call (double
  free) in :mod:`socket` when when a libc ``getaddrinfo()`` implementation
  leaves garbage in an output pointer when returning an error. Original
  patch by Sergey G. Brester.

- gh-issue-101143: Remove unused references to :class:`~asyncio.TimerHandle`
  in ``asyncio.base_events.BaseEventLoop._add_callback``.

- gh-issue-101144: Make :func:`zipfile.Path.open` and
  :func:`zipfile.Path.read_text` also accept ``encoding`` as a positional
  argument. This was the behavior in Python 3.9 and earlier. Earlier 3.10
  versions had a regression where supplying it as a positional argument
  would lead to a :exc:`TypeError`.

- gh-issue-100573: Fix a Windows :mod:`asyncio` bug with named pipes where a
  client doing ``os.stat()`` on the pipe would cause an error in the server
  that disabled serving future requests.

- gh-issue-90104: Avoid RecursionError on ``repr`` if a dataclass field
  definition has a cyclic reference.

- gh-issue-100689: Fix crash in :mod:`pyexpat` by statically allocating
  ``PyExpat_CAPI`` capsule.

- gh-issue-100740: Fix ``unittest.mock.Mock`` not respecting the spec for
  attribute names prefixed with ``assert``.

- gh-issue-86508: Fix :func:`asyncio.open_connection` to skip binding to
  local addresses of different family. Patch by Kumar Aditya.

- gh-issue-100287: Fix the interaction of :func:`unittest.mock.seal` with
  :class:`unittest.mock.AsyncMock`.

- gh-issue-100474: :mod:`http.server` now checks that an index page is
  actually a regular file before trying to serve it.  This avoids issues
  with directories named ``index.html``.

- gh-issue-100160: Remove any deprecation warnings in
  :func:`asyncio.get_event_loop`. They are deferred to Python 3.12.

- gh-issue-99952: Fix a reference undercounting issue in
  :class:`ctypes.Structure` with ``from_param()`` results larger than a C
  pointer.

- gh-issue-98778: Update :exc:`~urllib.error.HTTPError` to be initialized
  properly, even if the ``fp`` is ``None``. Patch by Dong-hee Na.

- gh-issue-83035: Fix :func:`inspect.getsource` handling of decorator calls
  with nested parentheses.

- gh-issue-99240: Fix double-free bug in Argument Clinic ``str_converter``
  by extracting memory clean up to a new ``post_parsing`` section.

- gh-issue-85267: Several improvements to :func:`inspect.signature`'s
  handling of ``__text_signature``. - Fixes a case where
  :func:`inspect.signature` dropped parameters - Fixes a case where
  :func:`inspect.signature` raised :exc:`tokenize.TokenError` - Allows
  :func:`inspect.signature` to understand defaults involving binary
  operations of constants - :func:`inspect.signature` is documented as only
  raising :exc:`TypeError` or :exc:`ValueError`, but sometimes raised
  :exc:`RuntimeError`. These cases now raise :exc:`ValueError` - Removed a
  dead code path

- gh-issue-96192: Fix handling of ``bytes`` :term:`path-like objects
  <path-like object>` in :func:`os.ismount()`.

- bpo-44817: Ignore WinError 53 (ERROR_BAD_NETPATH), 65
  (ERROR_NETWORK_ACCESS_DENIED) and 161 (ERROR_BAD_PATHNAME) when using
  ntpath.realpath().

- bpo-40447: Accept :class:`os.PathLike` (such as :class:`pathlib.Path`) in
  the ``stripdir`` arguments of :meth:`compileall.compile_file` and
  :meth:`compileall.compile_dir`.

- bpo-36880: Fix a reference counting issue when a :mod:`ctypes` callback
  with return type :class:`~ctypes.py_object` returns ``None``, which could
  cause crashes.

Documentation
-------------

- gh-issue-100616: Document existing ``attr`` parameter to
  :func:`curses.window.vline` function in :mod:`curses`.

- gh-issue-100472: Remove claim in documentation that the ``stripdir``,
  ``prependdir`` and ``limit_sl_dest`` parameters of
  :func:`compileall.compile_dir` and :func:`compileall.compile_file` could
  be :class:`bytes`.

Tests
-----

- gh-issue-101334: ``test_tarfile`` has been updated to pass when run as a
  high UID.

- gh-issue-96002: Add functional test for Argument Clinic.

Build
-----

- gh-issue-101522: Allow overriding Windows dependencies versions and paths
  using MSBuild properties.

Windows
-------

- gh-issue-82052: Fixed an issue where writing more than 32K of Unicode
  output to the console screen in one go can result in mojibake.

- gh-issue-100180: Update Windows installer to OpenSSL 1.1.1s

- bpo-43984: :meth:`winreg.SetValueEx` now leaves the target value untouched
  in the case of conversion errors. Previously, ``-1`` would be written in
  case of such errors.

macOS
-----

- gh-issue-100180: Update macOS installer to OpenSSL 1.1.1s

C API
-----

- gh-issue-99240: In argument parsing, after deallocating newly allocated
  memory, reset its pointer to NULL.


What's New in Python 3.10.9 final?
==================================

*Release date: 2022-12-06*

Security
--------

- gh-issue-100001: ``python -m http.server`` no longer allows terminal
  control characters sent within a garbage request to be printed to the
  stderr server log.

  This is done by changing the :mod:`http.server`
  :class:`BaseHTTPRequestHandler` ``.log_message`` method to replace control
  characters with a ``\xHH`` hex escape before printing.

- gh-issue-87604: Avoid publishing list of active per-interpreter audit
  hooks via the :mod:`gc` module

- gh-issue-98433: The IDNA codec decoder used on DNS hostnames by
  :mod:`socket` or :mod:`asyncio` related name resolution functions no
  longer involves a quadratic algorithm. This prevents a potential CPU
  denial of service if an out-of-spec excessive length hostname involving
  bidirectional characters were decoded. Some protocols such as
  :mod:`urllib` http ``3xx`` redirects potentially allow for an attacker to
  supply such a name.

- gh-issue-98739: Update bundled libexpat to 2.5.0

- gh-issue-98517: Port XKCP's fix for the buffer overflows in SHA-3
  (CVE-2022-37454).

- gh-issue-97514: On Linux the :mod:`multiprocessing` module returns to
  using filesystem backed unix domain sockets for communication with the
  *forkserver* process instead of the Linux abstract socket namespace.  Only
  code that chooses to use the :ref:`"forkserver" start method
  <multiprocessing-start-methods>` is affected.

  Abstract sockets have no permissions and could allow any user on the
  system in the same `network namespace
  <https://man7.org/linux/man-pages/man7/network_namespaces.7.html>`_ (often
  the whole system) to inject code into the multiprocessing *forkserver*
  process. This was a potential privilege escalation. Filesystem based
  socket permissions restrict this to the *forkserver* process user as was
  the default in Python 3.8 and earlier.

  This prevents Linux `CVE-2022-42919
  <https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-42919>`_.

Core and Builtins
-----------------

- gh-issue-99578: Fix a reference bug in :func:`_imp.create_builtin()` after
  the creation of the first sub-interpreter for modules ``builtins`` and
  ``sys``. Patch by Victor Stinner.

- gh-issue-99581: Fixed a bug that was causing a buffer overflow if the
  tokenizer copies a line missing the newline caracter from a file that is
  as long as the available tokenizer buffer. Patch by Pablo galindo

- gh-issue-96055: Update :mod:`faulthandler` to emit an error message with
  the proper unexpected signal number. Patch by Dong-hee Na.

- gh-issue-98852: Fix subscription of :class:`types.GenericAlias` instances
  containing bare generic types: for example ``tuple[A, T][int]``, where
  ``A`` is a generic type, and ``T`` is a type variable.

- gh-issue-98415: Fix detection of MAC addresses for :mod:`uuid` on certain
  OSs. Patch by Chaim Sanders

- gh-issue-92119: Print exception class name instead of its string
  representation when raising errors from :mod:`ctypes` calls.

- gh-issue-93696: Allow :mod:`pdb` to locate source for frozen modules in
  the standard library.

- bpo-31718: Raise :exc:`ValueError` instead of :exc:`SystemError` when
  methods of uninitialized :class:`io.IncrementalNewlineDecoder` objects are
  called. Patch by Oren Milman.

- bpo-38031: Fix a possible assertion failure in :class:`io.FileIO` when the
  opener returns an invalid file descriptor.

Library
-------

- gh-issue-100001: Also \ escape \s in the http.server
  BaseHTTPRequestHandler.log_message so that it is technically possible to
  parse the line and reconstruct what the original data was.  Without this a
  \xHH is ambiguious as to if it is a hex replacement we put in or the
  characters r"\x" came through in the original request line.

- gh-issue-93453: :func:`asyncio.get_event_loop` now only emits a
  deprecation warning when a new event loop was created implicitly. It no
  longer emits a deprecation warning if the current event loop was set.

- gh-issue-51524: Fix bug when calling trace.CoverageResults with valid
  infile.

- gh-issue-99645: Fix a bug in handling class cleanups in
  :class:`unittest.TestCase`.  Now ``addClassCleanup()`` uses separate lists
  for different ``TestCase`` subclasses, and ``doClassCleanups()`` only
  cleans up the particular class.

- gh-issue-97001: Release the GIL when calling termios APIs to avoid
  blocking threads.

- gh-issue-99341: Fix :func:`ast.increment_lineno` to also cover
  :class:`ast.TypeIgnore` when changing line numbers.

- gh-issue-74044: Fixed bug where :func:`inspect.signature` reported
  incorrect arguments for decorated methods.

- gh-issue-99275: Fix ``SystemError`` in :mod:`ctypes` when exception was
  not set during ``__initsubclass__``.

- gh-issue-99155: Fix :class:`statistics.NormalDist` pickle with ``0`` and
  ``1`` protocols.

- gh-issue-99134: Update the bundled copy of pip to version 22.3.1.

- gh-issue-99130: Apply bugfixes from `importlib_metadata 4.11.4
  <https://importlib-metadata.readthedocs.io/en/latest/history.html#v4-11-4>`_,
  namely: In ``PathDistribution._name_from_stem``, avoid including parts of
  the extension in the result. In ``PathDistribution._normalized_name``,
  ensure names loaded from the stem of the filename are also normalized,
  ensuring duplicate entry points by packages varying only by non-normalized
  name are hidden.

- gh-issue-83004: Clean up refleak on failed module initialisation in
  :mod:`_zoneinfo`

- gh-issue-83004: Clean up refleaks on failed module initialisation in in
  :mod:`_pickle`

- gh-issue-83004: Clean up refleak on failed module initialisation in
  :mod:`_io`.

- gh-issue-98897: Fix memory leak in :func:`math.dist` when both points
  don't have the same dimension. Patch by Kumar Aditya.

- gh-issue-98793: Fix argument typechecks in :func:`!_overlapped.WSAConnect`
  and :func:`!_overlapped.Overlapped.WSASendTo` functions.

- gh-issue-98740: Fix internal error in the :mod:`re` module which in very
  rare circumstances prevented compilation of a regular expression
  containing a :ref:`conditional expression <re-conditional-expression>`
  without the "else" branch.

- gh-issue-98703: Fix :meth:`asyncio.StreamWriter.drain` to call
  ``protocol.connection_lost`` callback only once on Windows.

- gh-issue-98624: Add a mutex to unittest.mock.NonCallableMock to protect
  concurrent access to mock attributes.

- gh-issue-89237: Fix hang on Windows in ``subprocess.wait_closed()`` in
  :mod:`asyncio` with :class:`~asyncio.ProactorEventLoop`. Patch by Kumar
  Aditya.

- gh-issue-98458: Fix infinite loop in unittest when a self-referencing
  chained exception is raised

- gh-issue-97928: :meth:`tkinter.Text.count` raises now an exception for
  options starting with "-" instead of silently ignoring them.

- gh-issue-97966: On ``uname_result``, restored expectation that ``_fields``
  and ``_asdict`` would include all six properties including ``processor``.

- gh-issue-98331: Update the bundled copies of pip and setuptools to
  versions 22.3 and 65.5.0 respectively.

- gh-issue-96035: Fix bug in :func:`urllib.parse.urlparse` that causes
  certain port numbers containing whitespace, underscores, plus and minus
  signs, or non-ASCII digits to be incorrectly accepted.

- gh-issue-98251: Allow :mod:`venv` to pass along :envvar:`PYTHON*`
  variables to ``ensurepip`` and ``pip`` when they do not impact path
  resolution

- gh-issue-98178: On macOS, fix a crash in :func:`syslog.syslog` in
  multi-threaded applications. On macOS, the libc ``syslog()`` function is
  not thread-safe, so :func:`syslog.syslog` no longer releases the GIL to
  call it. Patch by Victor Stinner.

- gh-issue-96151: Allow ``BUILTINS`` to be a valid field name for frozen
  dataclasses.

- gh-issue-98086: Make sure ``patch.dict()`` can be applied on async
  functions.

- gh-issue-88863: To avoid apparent memory leaks when
  :func:`asyncio.open_connection` raises, break reference cycles generated
  by local exception and future instances (which has exception instance as
  its member var). Patch by Dong Uk, Kang.

- gh-issue-93858: Prevent error when activating venv in nested fish
  instances.

- bpo-46364: Restrict use of sockets instead of pipes for stdin of
  subprocesses created by :mod:`asyncio` to AIX platform only.

- bpo-38523: :func:`shutil.copytree` now applies the
  *ignore_dangling_symlinks* argument recursively.

- bpo-36267: Fix IndexError in :class:`argparse.ArgumentParser` when a
  ``store_true`` action is given an explicit argument.

Documentation
-------------

- gh-issue-92892: Document that calling variadic functions with ctypes
  requires special care on macOS/arm64 (and possibly other platforms).

Tests
-----

- gh-issue-99892: Skip test_normalization() of test_unicodedata if it fails
  to download NormalizationTest.txt file from pythontest.net. Patch by
  Victor Stinner.

- bpo-34272: Some C API tests were moved into the new Lib/test/test_capi/
  directory.

Build
-----

- gh-issue-99086: Fix ``-Wimplicit-int``, ``-Wstrict-prototypes``, and
  ``-Wimplicit-function-declaration`` compiler warnings in
  :program:`configure` checks.

- gh-issue-99086: Fix ``-Wimplicit-int`` compiler warning in
  :program:`configure` check for ``PTHREAD_SCOPE_SYSTEM``.

- gh-issue-97731: Specify the full path to the source location for ``make
  docclean`` (needed for cross-builds).

- gh-issue-98671: Fix ``NO_MISALIGNED_ACCESSES`` being not defined for the
  SHA3 extension when ``HAVE_ALIGNED_REQUIRED`` is set. Allowing builds on
  hardware that unaligned memory accesses are not allowed.

Windows
-------

- gh-issue-99345: Use faster initialization functions to detect install
  location for Windows Store package

- gh-issue-98689: Update Windows builds to zlib v1.2.13.  v1.2.12 has
  CVE-2022-37434, but the vulnerable ``inflateGetHeader`` API is not used by
  Python.

- gh-issue-94328: Update Windows installer to use SQLite 3.39.4.

- bpo-40882: Fix a memory leak in
  :class:`multiprocessing.shared_memory.SharedMemory` on Windows.

macOS
-----

- gh-issue-94328: Update macOS installer to SQLite 3.39.4.

IDLE
----

- gh-issue-97527: Fix a bug in the previous bugfix that caused IDLE to not
  start when run with 3.10.8, 3.12.0a1, and at least Microsoft Python
  3.10.2288.0 installed without the Lib/test package.  3.11.0 was never
  affected.

Tools/Demos
-----------

- gh-issue-95731: Fix handling of module docstrings in
  :file:`Tools/i18n/pygettext.py`.


What's New in Python 3.10.8 final?
==================================

*Release date: 2022-10-11*

Security
--------

- gh-issue-97616: Fix multiplying a list by an integer (``list *= int``):
  detect the integer overflow when the new allocated length is close to the
  maximum size. Issue reported by Jordan Limor.  Patch by Victor Stinner.

- gh-issue-97612: Fix a shell code injection vulnerability in the
  ``get-remote-certificate.py`` example script. The script no longer uses a
  shell to run ``openssl`` commands. Issue reported and initial fix by Caleb
  Shortt. Patch by Victor Stinner.

- gh-issue-68966: The deprecated mailcap module now refuses to inject unsafe
  text (filenames, MIME types, parameters) into shell commands. Instead of
  using such text, it will warn and act as if a match was not found (or for
  test commands, as if the test failed).

Core and Builtins
-----------------

- gh-issue-96078: :func:`os.sched_yield` now release the GIL while calling
  sched_yield(2). Patch by Dong-hee Na.

- gh-issue-97943: Bugfix: :func:`PyFunction_GetAnnotations` should return a
  borrowed reference. It was returning a new reference.

- gh-issue-97591: Fixed a missing incref/decref pair in
  `Exception.__setstate__()`. Patch by Ofey Chan.

- gh-issue-96848: Fix command line parsing: reject :option:`-X
  int_max_str_digits <-X>` option with no value (invalid) when the
  :envvar:`PYTHONINTMAXSTRDIGITS` environment variable is set to a valid
  limit. Patch by Victor Stinner.

- gh-issue-95921: Fix overly-broad source position information for chained
  comparisons used as branching conditions.

- gh-issue-96821: Fix undefined behaviour in ``_testcapimodule.c``.

- gh-issue-95778: When :exc:`ValueError` is raised if an integer is larger
  than the limit, mention the :func:`sys.set_int_max_str_digits` function in
  the error message. Patch by Victor Stinner.

- gh-issue-96387: At Python exit, sometimes a thread holding the GIL can
  wait forever for a thread (usually a daemon thread) which requested to
  drop the GIL, whereas the thread already exited. To fix the race
  condition, the thread which requested the GIL drop now resets its request
  before exiting. Issue discovered and analyzed by Mingliang ZHAO. Patch by
  Victor Stinner.

- gh-issue-96864: Fix a possible assertion failure, fatal error, or
  :exc:`SystemError` if a line tracing event raises an exception while
  opcode tracing is enabled.

- gh-issue-96678: Fix undefined behaviour in C code of null pointer
  arithmetic.

- gh-issue-96641: Do not expose ``KeyWrapper`` in :mod:`_functools`.

- gh-issue-96611: When loading a file with invalid UTF-8 inside a multi-line
  string, a correct SyntaxError is emitted.

- gh-issue-95196: Disable incorrect pickling of the C implemented
  classmethod descriptors.

- gh-issue-96352: Fix :exc:`AttributeError` missing ``name`` and ``obj``
  attributes in :meth:`object.__getattribute__`. Patch by Philip Georgi.

- bpo-42316: Document some places where an assignment expression needs
  parentheses.

Library
-------

- gh-issue-87730: Wrap network errors consistently in urllib FTP support, so
  the test suite doesn't fail when a network is available but the public
  internet is not reachable.

- gh-issue-97825: Fixes :exc:`AttributeError` when
  :meth:`subprocess.check_output` is used with argument ``input=None`` and
  either of the arguments *encoding* or *errors* are used.

- gh-issue-96827: Avoid spurious tracebacks from :mod:`asyncio` when default
  executor cleanup is delayed until after the event loop is closed (e.g. as
  the result of a keyboard interrupt).

- gh-issue-97592: Avoid a crash in the C version of
  :meth:`asyncio.Future.remove_done_callback` when an evil argument is
  passed.

- gh-issue-97639: Remove ``tokenize.NL`` check from :mod:`tabnanny`.

- gh-issue-97545: Make Semaphore run faster.

- gh-issue-73588: Fix generation of the default name of
  :class:`tkinter.Checkbutton`. Previously, checkbuttons in different parent
  widgets could have the same short name and share the same state if
  arguments "name" and "variable" are not specified. Now they are globally
  unique.

- gh-issue-97005: Update bundled libexpat to 2.4.9

- gh-issue-85760: Fix race condition in :mod:`asyncio` where
  :meth:`~asyncio.SubprocessProtocol.process_exited` called before the
  :meth:`~asyncio.SubprocessProtocol.pipe_data_received` leading to
  inconsistent output. Patch by Kumar Aditya.

- gh-issue-96819: Fixed check in :mod:`multiprocessing.resource_tracker`
  that guarantees that the length of a write to a pipe is not greater than
  ``PIPE_BUF``.

- gh-issue-96741: Corrected type annotation for dataclass attribute
  ``pstats.FunctionProfile.ncalls`` to be ``str``.

- gh-issue-96652: Fix the faulthandler implementation of
  ``faulthandler.register(signal, chain=True)`` if the ``sigaction()``
  function is not available: don't call the previous signal handler if it's
  NULL. Patch by Victor Stinner.

- gh-issue-96073: In :mod:`inspect`, fix overeager replacement of
  "``typing.``" in formatting annotations.

- gh-issue-90467: Fix :class:`asyncio.streams.StreamReaderProtocol` to keep
  a strong reference to the created task, so that it's not garbage collected

- gh-issue-96052: Fix handling compiler warnings (SyntaxWarning and
  DeprecationWarning) in :func:`codeop.compile_command` when checking for
  incomplete input. Previously it emitted warnings and raised a SyntaxError.
  Now it always returns ``None`` for incomplete input without emitting any
  warnings.

- gh-issue-91212: Fixed flickering of the turtle window when the tracer is
  turned off. Patch by Shin-myoung-serp.

- gh-issue-74116: Allow :meth:`asyncio.StreamWriter.drain` to be awaited
  concurrently by multiple tasks. Patch by Kumar Aditya.

- gh-issue-90155: Fix broken :class:`asyncio.Semaphore` when acquire is
  cancelled.

- gh-issue-92986: Fix :func:`ast.unparse` when ``ImportFrom.level`` is None

- gh-issue-91539: Improve performance of
  ``urllib.request.getproxies_environment`` when there are many environment
  variables

Documentation
-------------

- gh-issue-97741: Fix ``!`` in c domain ref target syntax via a ``conf.py``
  patch, so it works as intended to disable ref target resolution.

- gh-issue-95588: Clarified the conflicting advice given in the :mod:`ast`
  documentation about :func:`ast.literal_eval` being "safe" for use on
  untrusted input while at the same time warning that it can crash the
  process. The latter statement is true and is deemed unfixable without a
  large amount of work unsuitable for a bugfix. So we keep the warning and
  no longer claim that ``literal_eval`` is safe.

- gh-issue-93031: Update tutorial introduction output to use 3.10+
  SyntaxError invalid range.

Build
-----

- gh-issue-96729: Ensure that Windows releases built with
  ``Tools\msi\buildrelease.bat`` are upgradable to and from official Python
  releases.

Windows
-------

- gh-issue-97728: Fix possible crashes caused by the use of uninitialized
  variables when pass invalid arguments in :func:`os.system` on Windows and
  in Windows-specific modules (like ``winreg``).

- gh-issue-90989: Clarify some text in the Windows installer.

- gh-issue-96577: Fixes a potential buffer overrun in :mod:`msilib`.

macOS
-----

- gh-issue-97897: The macOS 13 SDK includes support for the ``mkfifoat`` and
  ``mknodat`` system calls. Using the ``dir_fd`` option with either
  :func:`os.mkfifo` or :func:`os.mknod` could result in a segfault if
  cpython is built with the macOS 13 SDK but run on an earlier version of
  macOS. Prevent this by adding runtime support for detection of these
  system calls ("weaklinking") as is done for other newer syscalls on macOS.


What's New in Python 3.10.7 final?
==================================

*Release date: 2022-09-05*

Security
--------

- gh-issue-95778: Converting between :class:`int` and :class:`str` in bases
  other than 2 (binary), 4, 8 (octal), 16 (hexadecimal), or 32 such as base
  10 (decimal) now raises a :exc:`ValueError` if the number of digits in
  string form is above a limit to avoid potential denial of service attacks
  due to the algorithmic complexity. This is a mitigation for
  `CVE-2020-10735
  <https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-10735>`_.

  This new limit can be configured or disabled by environment variable,
  command line flag, or :mod:`sys` APIs. See the :ref:`integer string
  conversion length limitation <int_max_str_digits>` documentation.  The
  default limit is 4300 digits in string form.

  Patch by Gregory P. Smith [Google] and Christian Heimes [Red Hat] with
  feedback from Victor Stinner, Thomas Wouters, Steve Dower, Ned Deily, and
  Mark Dickinson.

Core and Builtins
-----------------

- gh-issue-96187: Fixed a bug that caused ``_PyCode_GetExtra`` to return
  garbage for negative indexes. Patch by Pablo Galindo

- gh-issue-95876: Fix format string in
  ``_PyPegen_raise_error_known_location`` that can lead to memory corruption
  on some 64bit systems. The function was building a tuple with ``i`` (int)
  instead of ``n`` (Py_ssize_t) for Py_ssize_t arguments.

- gh-issue-95605: Fix misleading contents of error message when converting
  an all-whitespace string to :class:`float`.

- gh-issue-93592: ``coroutine.throw()`` now properly initializes the
  ``frame.f_back`` when resuming a stack of coroutines. This allows e.g.
  ``traceback.print_stack()`` to work correctly when an exception (such as
  ``CancelledError``) is thrown into a coroutine.

- gh-issue-94996: :func:`ast.parse` will no longer parse function
  definitions with positional-only params when passed ``feature_version``
  less than ``(3, 8)``. Patch by Shantanu Jain.

Library
-------

- gh-issue-68163: Correct conversion of :class:`numbers.Rational`'s to
  :class:`float`.

- gh-issue-96159: Fix a performance regression in logging
  TimedRotatingFileHandler. Only check for special files when the rollover
  time has passed.

- gh-issue-96175: Fix unused ``localName`` parameter in the ``Attr`` class
  in :mod:`xml.dom.minidom`.

- gh-issue-95609: Update bundled pip to 22.2.2.

- gh-issue-95231: Fail gracefully if :data:`~errno.EPERM` or
  :data:`~errno.ENOSYS` is raised when loading :mod:`crypt` methods. This
  may happen when trying to load ``MD5`` on a Linux kernel with :abbr:`FIPS
  (Federal Information Processing Standard)` enabled.

Documentation
-------------

- gh-issue-96098: Improve discoverability of the higher level
  concurrent.futures module by providing clearer links from the lower level
  threading and multiprocessing modules.

- gh-issue-95789: Update the default RFC base URL from deprecated
  tools.ietf.org to datatracker.ietf.org

- gh-issue-91207: Fix stylesheet not working in Windows CHM htmlhelp docs.
  Contributed by C.A.M. Gerlach.

- bpo-47115: The documentation now lists which members of C structs are part
  of the :ref:`Limited API/Stable ABI <stable>`.

Tests
-----

- gh-issue-95243: Mitigate the inherent race condition from using
  find_unused_port() in testSockName() by trying to find an unused port a
  few times before failing. Patch by Ross Burton.

Build
-----

- gh-issue-94682: Build and test with OpenSSL 1.1.1q

IDLE
----

- gh-issue-65802: Document handling of extensions in Save As dialogs.

- gh-issue-95191: Include prompts when saving Shell (interactive input and
  output).


What's New in Python 3.10.6 final?
==================================

*Release date: 2022-08-01*

Security
--------

- gh-issue-87389: :mod:`http.server`: Fix an open redirection vulnerability
  in the HTTP server when an URI path starts with ``//``.  Vulnerability
  discovered, and initial fix proposed, by Hamza Avvan.

- gh-issue-92888: Fix ``memoryview`` use after free when accessing the
  backing buffer in certain cases.

Core and Builtins
-----------------

- gh-issue-95355: ``_PyPegen_Parser_New`` now properly detects token memory
  allocation errors. Patch by Honglin Zhu.

- gh-issue-94938: Fix error detection in some builtin functions when keyword
  argument name is an instance of a str subclass with overloaded ``__eq__``
  and ``__hash__``. Previously it could cause SystemError or other undesired
  behavior.

- gh-issue-94949: :func:`ast.parse` will no longer parse parenthesized
  context managers when passed ``feature_version`` less than ``(3, 9)``.
  Patch by Shantanu Jain.

- gh-issue-94947: :func:`ast.parse` will no longer parse assignment
  expressions when passed ``feature_version`` less than ``(3, 8)``. Patch by
  Shantanu Jain.

- gh-issue-94869: Fix the column offsets for some expressions in multi-line
  f-strings :mod:`ast` nodes. Patch by Pablo Galindo.

- gh-issue-91153: Fix an issue where a :class:`bytearray` item assignment
  could crash if it's resized by the new value's :meth:`__index__` method.

- gh-issue-94329: Compile and run code with unpacking of extremely large
  sequences (1000s of elements). Such code failed to compile. It now
  compiles and runs correctly.

- gh-issue-94360: Fixed a tokenizer crash when reading encoded files with
  syntax errors from ``stdin`` with non utf-8 encoded text. Patch by Pablo
  Galindo

- gh-issue-94192: Fix error for dictionary literals with invalid expression
  as value.

- gh-issue-93964: Strengthened compiler overflow checks to prevent crashes
  when compiling very large source files.

- gh-issue-93671: Fix some exponential backtrace case happening with deeply
  nested sequence patterns in match statements. Patch by Pablo Galindo

- gh-issue-93021: Fix the :attr:`__text_signature__` for :meth:`__get__`
  methods implemented in C. Patch by Jelle Zijlstra.

- gh-issue-92930: Fixed a crash in ``_pickle.c`` from mutating collections
  during ``__reduce__`` or ``persistent_id``.

- gh-issue-92914: Always round the allocated size for lists up to the
  nearest even number.

- gh-issue-92858: Improve error message for some suites with syntax error
  before ':'

Library
-------

- gh-issue-95339: Update bundled pip to 22.2.1.

- gh-issue-95045: Fix GC crash when deallocating ``_lsprof.Profiler`` by
  untracking it before calling any callbacks. Patch by Kumar Aditya.

- gh-issue-95087: Fix IndexError in parsing invalid date in the :mod:`email`
  module.

- gh-issue-95199: Upgrade bundled setuptools to 63.2.0.

- gh-issue-95194: Upgrade bundled pip to 22.2.

- gh-issue-93899: Fix check for existence of :data:`os.EFD_CLOEXEC`,
  :data:`os.EFD_NONBLOCK` and :data:`os.EFD_SEMAPHORE` flags on older kernel
  versions where these flags are not present. Patch by Kumar Aditya.

- gh-issue-95166: Fix :meth:`concurrent.futures.Executor.map` to cancel the
  currently waiting on future on an error - e.g. TimeoutError or
  KeyboardInterrupt.

- gh-issue-93157: Fix :mod:`fileinput` module didn't support ``errors``
  option when ``inplace`` is true.

- gh-issue-94821: Fix binding of unix socket to empty address on Linux to
  use an available address from the abstract namespace, instead of "\0".

- gh-issue-94736: Fix crash when deallocating an instance of a subclass of
  ``_multiprocessing.SemLock``. Patch by Kumar Aditya.

- gh-issue-94637: :meth:`SSLContext.set_default_verify_paths` now releases
  the GIL around ``SSL_CTX_set_default_verify_paths`` call. The function
  call performs I/O and CPU intensive work.

- gh-issue-94510: Re-entrant calls to :func:`sys.setprofile` and
  :func:`sys.settrace` now raise :exc:`RuntimeError`. Patch by Pablo
  Galindo.

- gh-issue-92336: Fix bug where :meth:`linecache.getline` fails on bad files
  with :exc:`UnicodeDecodeError` or :exc:`SyntaxError`. It now returns an
  empty string as per the documentation.
