# CodeCeption-Ant
A set of targets to test projects with CodeCeption using Ant. To be used mostly in CI systems.

# How to use it
This CodeCeption Ant project comes with a couple of pre-defined targets and a MacroDef.

The simplest use you can make of it is by including it and then invoking it in your project as follows:

```xml
    <!-- include the codeception ant project file -->
    <include file="${basedir}/build/codeception.xml" as="codeception"/>

    <!-- invoke it by creating a dependency on any of your targets -->
    <target name="build"
            depends="codeception.run-tests" />
```

`codeception.run-tests` will invoke codeception twice: first with the `build` parameter to build all the needed modules, and then with the `run` parameter to execute the tests.

You can also call the MacroDef and build any other call sequence if needed:

```xml
    <run suites="${codeception.suites}" options="${codeception.options}"/>
```

## Parameters

By default the project will invoke codeception as `codecept run --coverage-html`.

You can customise the options by setting `codeception.options` and `codeception.suites` at runtime:

```
$ ant -Dcodeception.suites="unit,functional" -Dcodeception.options="--xml --coverage-xml" build
```

Depending on your project, you might want to customise some other properties:

```xml
    <property name="tests.basedir" value="${basedir}/tests"/>
    <property name="codeception.basedir" value="${tests.basedir}/codeception"/>
    <property name="codeception.script" value="${basedir}/vendor/bin/codecept"/>
```

- `tests.basedir` the base test dir
- `codeception.basedir` where codeception tests are found
- `codeception.script` where the executable of CodeCeption is

The project will halt in case the executable is not found.

# Contributions are welcome

Please contribute by opening an issue or by forking and issuing a Pull Request.

If you want to do a Pull request, please be sure to read the following article first:
[How to write the perfect pull request](https://github.com/blog/1943-how-to-write-the-perfect-pull-request).
