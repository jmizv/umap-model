# umap-model
Create a uMap (http://umap.openstreetmap.fr) via Java.

➡️ Find the code at [codeberg.org](https://codeberg.org/jmizv/umap-model). 🧊

This library uses [Immutables](https://immutables.github.io/) for building
the objects.

## Usage

Create a simple map:

```java
var geometry = LineStringGeometry.of(List.of(new double[]{14.3804,52.5342},new double[]{14.8932,52.6739}));
var properties = FeatureProperties.of("My line", UmapOptions.PolygonGeometryUmapOptions.of("Red"));
var feature = Feature.of(properties, geometry);
var features = List.of(feature);
var layer = Layer.of("My features", features);
var layers = List.of(layer);
var initialMapPosition = PointGeometry.of(new double[]{14.8,52.5});
var map = Umap.of("My awesome map", initialMapPosition, layers);
```

Having now a `map` you could use your favorite JSON library to generate
a JSON document which could be imported to uMap. For example with GSON:

```java
try (PrintWriter out = new PrintWriter(new BufferedWriter(new FileWriter("c:\\temp\\test.umap", StandardCharsets.UTF_8)))) {
    new Gson().toJson(map, out);
} catch (IOException e) {
    throw new RuntimeException(e);
}
```
