---
title: iClient 3D in Vite
date: 2023-10-20T09:04:57.704Z
---
using iClient 3D in vite is tricky. because:
1. typing is missing few things, such as OpenStreetMapImageryProvider
2. can not be directly imported

solution:
1. create additional declaration file `Cesium-es6.d.ts` like this
```ts
declare module "@supermap/iclient3d-webgl/Cesium/Cesium-es6" {
  export namespace OpenStreetMapImageryProvider {
    /**
     * Initialization options for the OpenStreetMapImageryProvider constructor
     * @property [url = 'https://a.tile.openstreetmap.org'] - The OpenStreetMap server url.
     * @property [fileExtension = 'png'] - The file extension for images on the server.
     * @property [rectangle = Rectangle.MAX_VALUE] - The rectangle of the layer.
     * @property [minimumLevel = 0] - The minimum level-of-detail supported by the imagery provider.
     * @property [maximumLevel] - The maximum level-of-detail supported by the imagery provider, or undefined if there is no limit.
     * @property [ellipsoid] - The ellipsoid.  If not specified, the WGS84 ellipsoid is used.
     * @property [credit = 'MapQuest, Open Street Map and contributors, CC-BY-SA'] - A credit for the data source, which is displayed on the canvas.
     */
    interface ConstructorOptions {
      url?: string
      fileExtension?: string
      rectangle?: Rectangle
      minimumLevel?: number
      maximumLevel?: number
      ellipsoid?: Ellipsoid
      credit?: Credit | string
    }
  }

  /**
   * An imagery provider that provides tiled imagery hosted by OpenStreetMap
   * or another provider of Slippy tiles.  The default url connects to OpenStreetMap's volunteer-run
   * servers, so you must conform to their
   * {@link http://wiki.openstreetmap.org/wiki/Tile_usage_policy|Tile Usage Policy}.
   * @example
   * var osm = new Cesium.OpenStreetMapImageryProvider({
   *     url : 'https://a.tile.openstreetmap.org/'
   * });
   * @param options - Object describing initialization options
   */
  export class OpenStreetMapImageryProvider extends UrlTemplateImageryProvider {
    constructor(options: OpenStreetMapImageryProvider.ConstructorOptions)
  }

  export class DataSource {
    constructor()
    /**
     * Gets a human-readable name for this instance.
     */
    name: string
    /**
     * Gets the preferred clock settings for this data source.
     */
    clock: DataSourceClock
    /**
     * Gets the collection of {@link Entity} instances.
     */
    entities: EntityCollection
    /**
     * Gets a value indicating if the data source is currently loading data.
     */
    isLoading: boolean
    /**
     * Gets an event that will be raised when the underlying data changes.
     */
    changedEvent: Event
    /**
     * Gets an event that will be raised if an error is encountered during processing.
     */
    errorEvent: Event
    /**
     * Gets an event that will be raised when the value of isLoading changes.
     */
    loadingEvent: Event
    /**
     * Gets whether or not this data source should be displayed.
     */
    show: boolean
    /**
     * Gets or sets the clustering options for this data source. This object can be shared between multiple data sources.
     */
    clustering: EntityCluster
    /**
     * Updates the data source to the provided time.  This function is optional and
     * is not required to be implemented.  It is provided for data sources which
     * retrieve data based on the current animation time or scene state.
     * If implemented, update will be called by {@link DataSourceDisplay} once a frame.
     * @param time - The simulation time.
     * @returns True if this data source is ready to be displayed at the provided time, false otherwise.
     */
    update(time: JulianDate): boolean
  }

  export class GeoJsonDataSource {
    constructor(name?: string)
    /**
     * Creates a Promise to a new instance loaded with the provided GeoJSON or TopoJSON data.
     * @param data - A url, GeoJSON object, or TopoJSON object to be loaded.
     * @param [options] - An object specifying configuration options
     * @returns A promise that will resolve when the data is loaded.
     */
    static load(
      data: Resource | string | any,
      options?: GeoJsonDataSource.LoadOptions
    ): Promise<GeoJsonDataSource>
    /**
     * Gets or sets the default size of the map pin created for each point, in pixels.
     */
    static markerSize: number
    /**
     * Gets or sets the default symbol of the map pin created for each point.
     * This can be any valid {@link http://mapbox.com/maki/|Maki} identifier, any single character,
     * or blank if no symbol is to be used.
     */
    static markerSymbol: string
    /**
     * Gets or sets the default color of the map pin created for each point.
     */
    static markerColor: Color
    /**
     * Gets or sets the default color of polylines and polygon outlines.
     */
    static stroke: Color
    /**
     * Gets or sets the default width of polylines and polygon outlines.
     */
    static strokeWidth: number
    /**
     * Gets or sets default color for polygon interiors.
     */
    static fill: Color
    /**
     * Gets or sets default of whether to clamp to the ground.
     */
    static clampToGround: boolean
    /**
     * Gets an object that maps the name of a crs to a callback function which takes a GeoJSON coordinate
     * and transforms it into a WGS84 Earth-fixed Cartesian.  Older versions of GeoJSON which
     * supported the EPSG type can be added to this list as well, by specifying the complete EPSG name,
     * for example 'EPSG:4326'.
     */
    static crsNames: any
    /**
     * Gets an object that maps the href property of a crs link to a callback function
     * which takes the crs properties object and returns a Promise that resolves
     * to a function that takes a GeoJSON coordinate and transforms it into a WGS84 Earth-fixed Cartesian.
     * Items in this object take precedence over those defined in <code>crsLinkHrefs</code>, assuming
     * the link has a type specified.
     */
    static crsLinkHrefs: any
    /**
     * Gets an object that maps the type property of a crs link to a callback function
     * which takes the crs properties object and returns a Promise that resolves
     * to a function that takes a GeoJSON coordinate and transforms it into a WGS84 Earth-fixed Cartesian.
     * Items in <code>crsLinkHrefs</code> take precedence over this object.
     */
    static crsLinkTypes: any
    /**
     * Gets or sets a human-readable name for this instance.
     */
    name: string
    /**
     * This DataSource only defines static data, therefore this property is always undefined.
     */
    clock: DataSourceClock
    /**
     * Gets the collection of {@link Entity} instances.
     */
    entities: EntityCollection
    /**
     * Gets a value indicating if the data source is currently loading data.
     */
    isLoading: boolean
    /**
     * Gets an event that will be raised when the underlying data changes.
     */
    changedEvent: Event
    /**
     * Gets an event that will be raised if an error is encountered during processing.
     */
    errorEvent: Event
    /**
     * Gets an event that will be raised when the data source either starts or stops loading.
     */
    loadingEvent: Event
    /**
     * Gets whether or not this data source should be displayed.
     */
    show: boolean
    /**
     * Gets or sets the clustering options for this data source. This object can be shared between multiple data sources.
     */
    clustering: EntityCluster
    /**
     * Gets the credit that will be displayed for the data source
     */
    credit: Credit
    /**
     * Asynchronously loads the provided GeoJSON or TopoJSON data, replacing any existing data.
     * @param data - A url, GeoJSON object, or TopoJSON object to be loaded.
     * @param [options] - An object with the following properties:
     * @param [options.sourceUri] - Overrides the url to use for resolving relative links.
     * @param [options.describe = GeoJsonDataSource.defaultDescribeProperty] - A function which returns a Property object (or just a string),
     *                                                                                which converts the properties into an html description.
     * @param [options.markerSize = GeoJsonDataSource.markerSize] - The default size of the map pin created for each point, in pixels.
     * @param [options.markerSymbol = GeoJsonDataSource.markerSymbol] - The default symbol of the map pin created for each point.
     * @param [options.markerColor = GeoJsonDataSource.markerColor] - The default color of the map pin created for each point.
     * @param [options.stroke = GeoJsonDataSource.stroke] - The default color of polylines and polygon outlines.
     * @param [options.strokeWidth = GeoJsonDataSource.strokeWidth] - The default width of polylines and polygon outlines.
     * @param [options.fill = GeoJsonDataSource.fill] - The default color for polygon interiors.
     * @param [options.clampToGround = GeoJsonDataSource.clampToGround] - true if we want the features clamped to the ground.
     * @param [options.credit] - A credit for the data source, which is displayed on the canvas.
     * @returns a promise that will resolve when the GeoJSON is loaded.
     */
    load(
      data: Resource | string | any,
      options?: {
        sourceUri?: string
        describe?: GeoJsonDataSource.describe
        markerSize?: number
        markerSymbol?: string
        markerColor?: Color
        stroke?: Color
        strokeWidth?: number
        fill?: Color
        clampToGround?: boolean
        credit?: Credit | string
      }
    ): Promise<GeoJsonDataSource>
    /**
     * Updates the data source to the provided time.  This function is optional and
     * is not required to be implemented.  It is provided for data sources which
     * retrieve data based on the current animation time or scene state.
     * If implemented, update will be called by {@link DataSourceDisplay} once a frame.
     * @param time - The simulation time.
     * @returns True if this data source is ready to be displayed at the provided time, false otherwise.
     */
    update(time: JulianDate): boolean
  }

  export class DataSourceCollection {
    constructor()
    /**
     * Gets the number of data sources in this collection.
     */
    readonly length: number
    /**
     * An event that is raised when a data source is added to the collection.
     * Event handlers are passed the data source that was added.
     */
    readonly dataSourceAdded: Event
    /**
     * An event that is raised when a data source is removed from the collection.
     * Event handlers are passed the data source that was removed.
     */
    readonly dataSourceRemoved: Event
    /**
     * An event that is raised when a data source changes position in the collection.  Event handlers are passed the data source
     * that was moved, its new index after the move, and its old index prior to the move.
     */
    readonly dataSourceMoved: Event
    /**
     * Adds a data source to the collection.
     * @param dataSource - A data source or a promise to a data source to add to the collection.
     *                                        When passing a promise, the data source will not actually be added
     *                                        to the collection until the promise resolves successfully.
     * @returns A Promise that resolves once the data source has been added to the collection.
     */
    add(dataSource: DataSource | Promise<DataSource>): Promise<DataSource>
    /**
     * Removes a data source from this collection, if present.
     * @param dataSource - The data source to remove.
     * @param [destroy = false] - Whether to destroy the data source in addition to removing it.
     * @returns true if the data source was in the collection and was removed,
     *                    false if the data source was not in the collection.
     */
    remove(dataSource: DataSource, destroy?: boolean): boolean
    /**
     * Removes all data sources from this collection.
     * @param [destroy = false] - whether to destroy the data sources in addition to removing them.
     */
    removeAll(destroy?: boolean): void
    /**
     * Checks to see if the collection contains a given data source.
     * @param dataSource - The data source to check for.
     * @returns true if the collection contains the data source, false otherwise.
     */
    contains(dataSource: DataSource): boolean
    /**
     * Determines the index of a given data source in the collection.
     * @param dataSource - The data source to find the index of.
     * @returns The index of the data source in the collection, or -1 if the data source does not exist in the collection.
     */
    indexOf(dataSource: DataSource): number
    /**
     * Gets a data source by index from the collection.
     * @param index - the index to retrieve.
     * @returns The data source at the specified index.
     */
    get(index: number): DataSource
    /**
     * Gets a data source by name from the collection.
     * @param name - The name to retrieve.
     * @returns A list of all data sources matching the provided name.
     */
    getByName(name: string): DataSource[]
    /**
     * Raises a data source up one position in the collection.
     * @param dataSource - The data source to move.
     */
    raise(dataSource: DataSource): void
    /**
     * Lowers a data source down one position in the collection.
     * @param dataSource - The data source to move.
     */
    lower(dataSource: DataSource): void
    /**
     * Raises a data source to the top of the collection.
     * @param dataSource - The data source to move.
     */
    raiseToTop(dataSource: DataSource): void
    /**
     * Lowers a data source to the bottom of the collection.
     * @param dataSource - The data source to move.
     */
    lowerToBottom(dataSource: DataSource): void
    /**
     * Returns true if this object was destroyed; otherwise, false.
     * If this object was destroyed, it should not be used; calling any function other than
     * <code>isDestroyed</code> will result in a {@link DeveloperError} exception.
     * @returns true if this object was destroyed; otherwise, false.
     */
    isDestroyed(): boolean
    /**
     * Destroys the resources held by all data sources in this collection.  Explicitly destroying this
     * object allows for deterministic release of WebGL resources, instead of relying on the garbage
     * collector. Once this object is destroyed, it should not be used; calling any function other than
     * <code>isDestroyed</code> will result in a {@link DeveloperError} exception.  Therefore,
     * assign the return value (<code>undefined</code>) to the object as done in the example.
     * @example
     * dataSourceCollection = dataSourceCollection && dataSourceCollection.destroy();
     */
    destroy(): void
  }
}

```

2. exclude iclient3d from optimizedeps, like this
```ts
export default defineConfig({
...,
 optimizeDeps: {
    include: ["vue", "vue-router", "@vueuse/core"],
    exclude: ["vue-demi", "@supermap/iclient3d-webgl", "src/libs/sm/iclient-3D/Cesium-es6.js"]
  }
...
})
```