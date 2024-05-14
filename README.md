![license](https://img.shields.io/github/license/danieletorelli/sbt-was-component?style=for-the-badge)
[![build](https://img.shields.io/github/actions/workflow/status/danieletorelli/sbt-wasm-component/ci.yml?branch=main&style=for-the-badge)](https://github.com/danieletorelli/sbt-wasm-component/actions?query=workflow%3A%22CI%22+branch%3Amain)
[![release](https://img.shields.io/github/v/release/danieletorelli/sbt-component-release?style=for-the-badge)](https://github.com/danieletorelli/librespeed-cli/releases/latest)
![version](https://img.shields.io/maven-central/v/io.github.danieletorelli/sbt-wasm-component?style=for-the-badge)

sbt-wasm-component
==================

Avoid any boilerplate in your project by using just one annotation to export your Golem worker from Scala to JS.

Setup
-----

Add sbt-wasm-component as a dependency in `project/plugins.sbt`:

```scala
addSbtPlugin("cloud.golem" % "sbt-wasm-component" % "x.y.z")
```

Usage
-----

The WASM component plugin is automatically loaded, it just needs to be enabled with `enablePlugins(WasmComponentPlugin)` in your `build.sbt`:

```scala
ThisBuild / version := "0.1.0-SNAPSHOT"
ThisBuild / scalaVersion := "2.13.13"

lazy val root = (project in file("."))
  .enablePlugins(WasmComponentPlugin)
```

Then you will be able to annotate your Golem worker object with the `@cloud.golem.WitExport` annotation:

```scala
package example

@cloud.golem.WitExport
object ShoppingCart { self =>

  def initializeCart(userId: String): String = {
    println(s"Initializing cart for user $userId")
    if (math.random() > 0.1) userId
    else "Error while initializing cart"
  }
  
  // ...

}

```

Once done that, it will be enough to run `sbt wasmComponent` and the plugin will take care of exporting your worker in WASM.

