# OSMCity

OSMCity is a project made on Unity by myself about reconstructing buildings in cities from OpenStreetMap data, at an estimated height.

The User manual and State of the art are written in french.

**Tech stack:** C# · .NET · ML.NET · OsmSharp · Unity · ProBuilder

## Pipeline

```mermaid
flowchart LR
    A["1. OSM PBF extract<br/>(.osm.pbf)"] --> B["2. XML export<br/>(OsmSharp)"]
    B --> C["3. Height prediction<br/>(ML.NET FastTree)"]
    C --> D["4. Unity loaders<br/>(BuildingLoader, HighwayLoader)"]
    D --> E["5. 3D meshes<br/>(ProBuilder buildings, roofs, roads)"]
```

1. **PBF**: a `.osm.pbf` extract of the target area is read with OsmSharp.
2. **XML**: it is exported to the XML files (nodes, ways, relations, tags) stored in `Assets/Resources/XmlFiles/`.
3. **Height prediction**: offline, buildings without a `height` tag get one predicted by an ML.NET regression model trained on the tagged ones (area, perimeter, floors, neighbors...), written to `Assets/Resources/TxtFiles/`.
4. **Loaders**: in Unity, `BuildingLoader` and `HighwayLoader` stream the XML files into an OSM object graph and read the predicted heights.
5. **3D meshes**: each building and highway is turned into a ProBuilder mesh, with roofs, colors and materials taken from its OSM tags.

## Screenshots

![liechtenstein](https://user-images.githubusercontent.com/25984451/221054501-be19c9df-d993-4207-985e-a63b00078778.png)
Here, an aerial view of the city of Vaduz in Liechtenstein inside my 3D model.

![luxembourg](https://github.com/user-attachments/assets/88e8a02d-356f-4965-bbb1-9e14a007c0d5)
Here, an aerial view of the city of Luxembourg inside my 3D model with many buildings and highways.
