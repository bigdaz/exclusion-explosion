### Exclusion-explosion

Simple project that demonstrates a potential explosion of unmerged exclusions.

To see the exclusions, put a breakpoint here: https://github.com/gradle/gradle/blob/193a6c24141094bfe8cb71eab1eafe22c90bcb2b/subprojects/dependency-management/src/main/java/org/gradle/api/internal/artifacts/ivyservice/resolveengine/graph/builder/NodeState.java#L679

And run `gradle dependencies --configuration compileClasspath --no-daemon -Dorg.gradle.debug=true`.

The resulting exclude rule looks like:
```
{all of [
  {any of [
    {exclude group = 'G1'},
    { module ids = [A:B, A:C]}]},
  {any of [
    {exclude group = 'G1'},
    { module ids = [A:B, A:D]}
  ]}
]}
```
