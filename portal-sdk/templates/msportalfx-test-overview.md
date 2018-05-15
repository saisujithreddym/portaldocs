## Overview

MsPortalFx-Test is an end-to-end test framework that runs tests against the Microsoft Azure Portal interacting with it as a user would. 

### Goals

- Strive for zero breaking changes to partner team CI
- Develop tests in the same language as the extension
- Focus on partner needs rather than internal Portal needs
- Distributed independently from the SDK
- Uses an open source contribution model
- Performant
- Robust
- Great Docs

### General Architecture

3 layers of abstraction (note the names may change but the general idea should be the same).  There may also be some future refactoring to easily differentiate between the layers.
- Test layer 

    - Useful wrappers for testing common functionality.  Will retry if necessary.  Throws if the test/verification fails.  
    - Should be used in writing tests
    - Built upon the action and control layers
    - EG: parts.canPinAllBladeParts
    
- Action layer 

    - Performs an action and verifies it was successful.  Will retry if necessary.
    - Should be used in writing tests
    - Built upon the controls layer
    - EG: portal.openBrowseBlade
    
- Controls layer 

    - The basic controls used in the Portal (eg blades, checkboxes, textboxes, etc).  Little to no retry logic.  Should be used mainly for composing the actions and tests layers.
    - Should be used for writing test and action layers.  Should not be used directly by tests in most cases.
    - Built upon webdriver primitives
    - EG: part, checkbox, etc  
