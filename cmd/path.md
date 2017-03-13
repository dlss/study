@echo off
rem -------------------file path start-----------------
echo 01---- %cd%
echo 02---- %~f0
echo 03---- %~d0
echo 04---- %~p0
echo 05---- %~n0
echo 06---- %~x0
echo 07---- %~s0
echo 08---- %~a0
echo 09---- %~t0
echo 10---- %~z0       
echo 11---- %~dp0
echo 12---- %~nx0
echo 13---- %~fs0
echo 14---- %~ftza0

pushd .. 
SET parentPath=%CD%
popd
echo 15---- %parentPath%

rem 01---- C:\SourceCode\scripts
rem 02---- C:\SourceCode\scripts\study.bat
rem 03---- C:
rem 04---- \SourceCode\scripts\
rem 05---- study
rem 06---- .bat
rem 07---- C:\SOURCE~1\scripts\study.bat
rem 08---- --a--------
rem 09---- 12/06/2016 10:56 AM
rem 10---- 404
rem 11---- C:\SourceCode\scripts\
rem 12---- study.bat
rem 13---- C:\SOURCE~1\scripts\study.bat
rem 14---- --a-------- 12/06/2016 10:56 AM 404 C:\SourceCode\scripts\study.bat
rem 15---- C:\SourceCode
rem -------------------file path end-----------------
