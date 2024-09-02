---
title: Typescript Tricks
draft: false
publish: true
tags:
  - typescript
date: 2024-09-02
---
## Using a Record Type for Dynamic Keys

```typescript
const albumAwards: Record<string, boolean> = {};

albumAwards.Grammy = true;
```

That is shorter than:
```typescript
type AlbumAwards = {
	[keys: String]: boolean;
}

const albumAwards: AlbumAwards = {}

albumAwards.Grammy = true;
```

## Combining Know and Dynamic Keys

```typescript
interface BaseAwards {
	Grammy: boolean;
	MercuryPrize: boolean;
	Billboard: boolean;
}

interface ExtendedAlbumAwards extends BaseAwards {
	[award: string]: boolean;
}
```

Interface extension is preferable to intersections.

## PropertyKey
This is a global type for property keys

```typescript
// inside lib.es5.d.ts
declare type PropertyKey = string | number | symbol;
```

## Utility Types
### Partial
The Partial utility type lets you create a new object type from an existing one, except all of its properties are optional.
```typescript
interface Album {
  id: number;
  title: string;
  artist: string;
  releaseYear: number;
  genre: string;
}

type PartialAlbum = Partial<Album>;
```

### Required
On the opposite side of Partial is the Required type, which makes sure all of the properties of a given object type are required.
```typescript
interface Album {
  title: string;
  artist: string;
  releaseYear?: number;
  genre?: string;
}

type RequiredAlbum = Required<Album>;
```

### Pick
The Pick utility type allows you to create a new object type by picking certain properties from an existing object.

```typescript
type AlbumData = Pick<Album, "title" | "artist">;
```

### Omit
The Omit helper type is kind of like the opposite of Pick. It allows you to create a new type by excluding a subset of properties from an existing type.
```typescript
type AlbumData = Omit<Album, "id" | "releaseYear" | "genre">;
```

### Readonly
If you want to specify that all properties of an object should be read-only, TypeScript provides a type helper called Readonly.

```typescript
const readOnlyWhiteAlbum: Readonly<Album> = {
  title: "The Beatles (White Album)",
  artist: "The Beatles",
  status: "staff-pick",
};
```

### ReturnType

The ReturnType utility type extracts the return type from a given function:
```typescript
type SellAlbumReturn = ReturnType<typeof sellAlbum>;
```

### Parameters

The Parameters utility type extracts the parameters from a given function type and returns them as a tuple.

```typescript
function sellAlbum(album: Album, price: number, quantity: number) {
  return price * quantity;
}

type SellAlbumParams = Parameters<typeof sellAlbum>;
```

### Awaited

The Awaited utility type is used to unwrap the Promise type and provide the type of the resolved value. Think of it as a shortcut similar to using await or .then() methods.

```typescript
type AlbumPromise = Promise<Album>;

type AlbumResolved = Awaited<AlbumPromise>;
```

References: [[Typescript]] [[Javascript]]