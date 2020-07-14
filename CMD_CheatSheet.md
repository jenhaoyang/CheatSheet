# 暫停錯誤
-- do stuff --

CALL :CHECK_FAIL

-- do more stuff --

CALL :CHECK_FAIL

:: ======== FN ======
GOTO :EOF

:: /// check if the app has failed
:CHECK_FAIL
[AT]echo off
if NOT ["%errorlevel%"]==["0"] (
    pause
    exit /b %errorlevel%
)
