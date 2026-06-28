# Reproduction notes for issue #13367

Built and installed MiniUPnPc locally with CMake using:

cmake ../miniupnpc -DCMAKE_INSTALL_PREFIX=/tmp/miniupnpc-install
cmake --build .
cmake --install .

Then inspected the generated CMake package files with:

grep -R "INTERFACE_INCLUDE_DIRECTORIES" /tmp/miniupnpc-install/lib/cmake/miniupnpc

Observed result:

libminiupnpc-static.cmake and libminiupnpc-shared.cmake both export:

INTERFACE_INCLUDE_DIRECTORIES "${_IMPORT_PREFIX}/include/miniupnpc;${_IMPORT_PREFIX}/include"

On Haiku, this expands to /boot/system/include/miniupnpc, which matches the incorrect include path described in the issue.
