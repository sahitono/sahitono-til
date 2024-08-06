---
title: Flyway 10.6 failed migration
date: 2024-08-06T04:47:03.229Z
tags:
  - java
---
F﻿lyway failed to migrate on version 10.6  inside fatjar due to:

1﻿. migration file not automatically included in the fatjar

2﻿. invalid filename

t﻿he solution is to include the resource by adding this line in the gradle

`﻿``kt
sourceSets {
    main {
        resources.srcDir(project(":lib:database").sourceSets["main"].resources.srcDirs)
    }
}
`﻿``

a﻿nd then setup the `mergeServiceFiles`
https://github.com/flyway/flyway/issues/3811#issuecomment-1923760202
`﻿``kt
ktor {
    tasks {
        fatJar {
            shadowJar {
                mergeServiceFiles()
            }
        }
    }
}
`﻿``