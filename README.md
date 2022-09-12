# .NET 6.0 Class Library Template

##Generate Class Library Solution

Create a powershell script with the following
```
param([Int32]$projectName="SomeProject")

mkdir $projectName
cd $projectName

dotnet new sln
dotnet new gitignore

mkdir $projectName
cd $projectName
dotnet new classlib --no-restore

cd ..
dotnet sln add .\$projectName\$projectName.csproj

mkdir Tests
cd Tests

mkdir $projectName.UnitTests
cd $projectName.UnitTests
dotnet new xunit --no-restore
dotnet add $projectName.UnitTests.csproj reference ..\..\$projectName\$projectName.csproj
dotnet add package FluentAssertions --no-restore
dotnet add package NSubstitute --no-restore

cd ..
mkdir $projectName.IntegrationTests
cd $projectName.IntegrationTests
dotnet new xunit --no-restore
dotnet add $projectName.IntegrationTests.csproj reference ..\..\$projectName\$projectName.csproj
dotnet add package FluentAssertions --no-restore
dotnet add package NSubstitute --no-restore

cd ..\..
dotnet sln add .\Tests\$projectName.UnitTests\$projectName.UnitTests.csproj
dotnet sln add .\Tests\$projectName.IntegrationTests\$projectName.IntegrationTests.csproj
echo $projectName Created
```

Then run it from powershell with the first argument being the name for the Solution and Class Library project.

