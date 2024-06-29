# zipcode-detail-lookup

[![Build Status](https://github.com/reallymello/zipcode-detail-lookup/actions/workflows/node.js.yml/badge.svg)](https://github.com/reallymello/zipcode-detail-lookup/actions/workflows/node.js.yml)

![Line Coverage](./badges/badge-lines.svg)
![Statement Coverage](./badges/badge-statements.svg)
![Function Coverage](./badges/badge-functions.svg)
![Branch Coverage](./badges/badge-branches.svg)

Given a US Zip Code, this program returns the associated State, County, City, and other useful information; latitude, longitude, density, population, military designation, timezone.

The data source contains US states and territories.

The database is originally derived from the 2024 free-tier list provided by SimpleMaps.

## Installation

Install zipcode-detail-lookup as a dependency in your project.

```sh
npm install zipcode-detail-lookup --save
```

After, import it into your code at the top of your project

```ts
import { zip, searchBy, random } from 'zipcode-detail-lookup';
```

## Usage

Zip Code Lookup provides 3 functions; zip, random, and searchBy. zip and random return a single zip code object result whereas searchBy will return an array of matches.

### zip(zipCode: string)

```ts
const fll = zdl.zip(33316); // For returning an object for the 33316 Ft. Lauderdale zip code.
console.log(fll.state); // Florida
console.log(fll.stateAbbreviation); // FL
console.log(fll.county); // Broward
console.log(fll.city); // Fort Lauderdale
```

### random()

This will return a random zip code from the data set and will include all the properties as mentioned in the previous example (state, city, county, demographics, location, etc.)

```ts
const randomZip = zdl.random();

console.log(randomZip.zip); // Random zip code e.g. 11122
```

### searchBy({...searchParams: ISearchParams})

This method will let you search for any optional combination of criteria involving city, county, stateName, stateAbbreviation, military classification, and population count.

```ts
// To return an array of results matching the state abbreviation FL with population greather than 27000.
const searchResults = zdl.searchBy({
  stateAbbreviation: 'FL',
  population: 27000,
  populationOperator: '>',
});
```

You can optionally use any combination of these settings exposed on the interface.

```ts
interface ISearchParams {
  city?: string;
  county?: string;
  stateName?: string;
  stateAbbreviation?: string;
  militaryZip?: boolean;
  population?: number;
  populationOperator?: '<' | '>' | '=';
}
```
