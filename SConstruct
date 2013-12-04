#
# Build script for agent.
#

import sys
import subprocess


def build(target = None, source = None, env = None):
    """Proxy-target: build"""
    pass

def cleanup(target = None, source = None, env = None):
    """Removes generated artifacts"""
    # TODO clean up.
    pass

def createDist(target = None, source = None, env = None):
    """Create distributable for agent."""
    # TODO create.
    pass

def createPackage(target = None, source = None, env = None):
    """Create installable packages for supported operating systems."""

    retCode = 0
    retCode += _createDebPackage()
    retCode += _createRpmPackage()
    if retCode:
        return 1
    else:
        return 0

def runIntegrationTests(target, source, env):
    """Run integration tests."""
    # TODO run tests.
    pass

def runUnitTests(target, source, env):
    """Run unit tests."""

    retCode = subprocess.call(['python', 'run-tests.py'])
    if retCode:
        print "Unit tests failed!"
    return retCode

def _createDebPackage():
    # TODO create the package.
    print "\nCreating .deb package..."
    return 0

def _createRpmPackage():
    # TODO create the package.
    print "\nCreating .rpm package..."
    return 0

Help("""
Usage: scons command [command...]
where supported commands are:
all                 Runs all commands.
build               Runs unit tests and builds agent components.
clean               Removes generated artifacts.
dist                Creates distributable artifacts for agent.
package             Creates installable packages for supported OS distributions.
test                Runs unit tests.
test-integration    Runs integration tests.
""")

env = Environment()
env.Alias('all', ['.'])

unitTestTask = env.Command('test', None, Action(runUnitTests, "\n--- Running unit tests"))

integrationTestTask = env.Command(\
    'test-integration', \
    None, \
    Action(runIntegrationTests, "\n--- Running integration tests"))

buildTask = env.Command('build', None, Action(build, "\n--- Building"))
Depends(buildTask, unitTestTask)

packageTask = env.Command('package', None, Action(createPackage, "\n--- Creating install packages"))
Depends(packageTask, unitTestTask)

distTask = env.Command('dist', None, Action(createDist, "\n--- Creating distributables"))
Depends(distTask, unitTestTask)
Depends(distTask, packageTask)
Depends(distTask, integrationTestTask)

cleanTask = env.Command('clean', None, Action(cleanup, "\n--- Cleaning up"))

# task to run if no command specified.
Default(buildTask)