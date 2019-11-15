## Registry

[![Actions](https://github.com/wk-j/github-registry/workflows/Build/badge.svg)](https://github.com/wk-j/github-registry/actions)

```
nuget source Remove -Name wk-j
nuget source Remove -Name GitHub

nuget source Add -Name GitHub \
    -Source "https://nuget.pkg.github.com/wk-j/index.json" \
    -UserName wk-j \
    -Password $GITHUB_TOKEN

dotnet pack src/MyConsole/MyConsole.fsproj --output .publish

nuget push \
    -Source GitHub \
    .publish/MyConsole.0.1.0.nupkg

dotnet nuget push \
    --source https://nuget.pkg.github.com/wk-j/index.json \
    --api-key $GITHUB_TOKEN \
    (find . -name "MyConsole*.nupkg")

dotnet nuget push \
    --source https://nuget.pkg.github.com/wk-j/index.json \
    --api-key $GITHUB_TOKEN \
    .publish/MyConsole.19.11.14.1332.nupkg

cat ~/.config/NuGet/NuGet.Config

curl -vX PUT -u wk-j:$GITHUB_TOKEN -F package=@(find . -name "MyConsole*.nupkg") https://nuget.pkg.github.com/wk-j

```

## Issues

- https://github.community/t5/GitHub-API-Development-and/github-package-registry-not-compatible-with-dotnet-nuget-client/td-p/34776
- https://github.com/NuGet/Home/issues/8580