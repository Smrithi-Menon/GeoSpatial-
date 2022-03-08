def ckdnearest(gdA, gdB):
    """
    This functions take two geodataframes and searches for the nearest neighbor for each of the points in gdA given the 
    geolocations of gdB.
    
    Returns:
        GeoDataframe A spatially joined with nearest neighbour of GeoDataFrame B
    """
    nA = np.array(list(gdA.geometry.apply(lambda x: (x.x, x.y))))
    nB = np.array(list(gdB.geometry.apply(lambda x: (x.x, x.y))))
    btree = cKDTree(nB)
    dist, idx = btree.query(nA, k=1)
    gdB_nearest = gdB.iloc[idx].rename(columns={"geometry": "geometry_norm"}).reset_index(drop=True)
    gdf = pd.concat(
        [
            gdA.reset_index(drop=True),
            gdB_nearest,
            pd.Series(dist, name='dist')
        ], 
        axis=1)

    return gdf
