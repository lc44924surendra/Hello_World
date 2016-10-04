# Hello_World
Test Repository
This is testing file

@ECHO OFF
SET SQLLOG=%~dp0sql_log.txt
SET SQLSERVER=.
ECHO. Starting Script, Server: %SQLSERVER%, logging to : %SQLLOG%
ECHO.

CALL:runsql "1 Create Databases"
CALL:runsql "2 Create Schema"
CALL:runsql "3 Data\AA"
CALL:runsql "3 Data\BB"
CALL:runsql "3 Data\CC"
CALL:runsql "3 Data\DD"

EXIT /B %ERRORLEVEL%

::Function to run all SQL in a Directory
:runsql
echo.
echo. Executing Scripts in Directory:
echo. %~1
echo.
PUSHD %~1
for %%G in (*.sql) do echo. sqlcmd -S"%SQLSERVER%" -E -e -i"%%G"
for %%G in (*.sql) do echo. sqlcmd -S"%SQLSERVER%" -E -e -i"%%G" >> "%SQLLOG%"
for %%G in (*.sql) do sqlcmd -S"%SQLSERVER%" -E -e -i"%%G" >> "%SQLLOG%"
POPD
