# Green Gentrification in Glasgow

Is green gentrification happening in Glasgow? This project looks at private rents and neighbourhood deprivation between 2016 and 2024 to find out rent dynamics across the city's neighbourhoods.

 **[View the full report](https://sammigrewal.github.io/Green-Gentrification-Glasgow/Green_Gentrification_Glasgow.html)**

---

## Background

Green gentrification is when people on lower incomes are pushed out of areas near urban greenspace because wealthier residents move in. Most research looks at *newly built* greenspace. This project asks whether rents near Glasgow's *existing* parks rising fast enough to put lower-income residents at risk of displacement?

## Data

| Dataset | Source | Use |
|---|---|---|
| Private rental listings | Zoopla Plc (via the Urban Big Data Centre, under licence) | Weekly rent, location and property type |
| Scottish Index of Multiple Deprivation (SIMD) 2016 and 2020 | Scottish Government | Deprivation decile for each datazone |
| OS Open Greenspace | Ordnance Survey | Public parks and gardens |
| Data Zone boundaries 2011 | Scottish Government | Neighbourhood polygons for mapping |

> ⚠️ The Zoopla data is licensed and is not included in this repository. It was accessed under an end-user licence from the [Urban Big Data Centre](https://www.ubdc.ac.uk/).

## Method

1. **Load and merge.** Read the Zoopla rental extracts in chunks, keep only Glasgow City listings, and join them to SIMD deciles by postcode.
2. **Clean.** Keep only flats priced between £50 and £400 a week with 6 bedrooms or fewer.
3. **Explore.** Map rents against public parks, and plot median rent over time for each SIMD decile.
4. **Build PCA indices.** For each datazone, combine average median rent and SIMD decile into one index per period: 2016 (rents 2016–19 with SIMD 2016) and 2024 (rents 2020–24 with SIMD 2020). The change between the two indices measures how each neighbourhood moved.
5. **Cluster.** Group datazones on that index change with K-means, choosing K = 4 by the elbow method.
6. **Evaluate.** Check the clusters with silhouette scores and the Calinski–Harabasz score (3,964.79).

The analysis covers **616 of Glasgow's 746 datazones (82%)**. The rest had no listings in the data.

## Key findings

- **Rents rose sharply after 2020.** In the most deprived decile, median rent rose 11% from 2016 to 2019 and 43% from 2020 to 2024.
- **Four neighbourhood types emerged:**

  | Cluster | Description |
  |---|---|
  | 0 | Relatively stable, with rents up 17.6% (below the national rise) |
  | 1 | **Rents rising fast, up 89.2%. Most at risk of gentrification** (39 datazones) |
  | 2 | Previously expensive areas where rents have fallen and deprivation has risen (57 datazones) |
  | 3 | Rents rising slowly |

- **Fast-rising areas sit near large parks** such as Pollok Country Park, Bellahouston Park, Cowlairs Park, Sighthill Park and Springburn Park. They are more common in the south of the city.
- **Limitations.** Without data on who moves in and out of each area, the analysis can't show that displacement is actually happening. SIMD deciles also changed little over the period, so the model mostly responds to rent changes.
