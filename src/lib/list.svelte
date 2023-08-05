<script lang="ts">
  import { faker } from "@faker-js/faker";

  const LocationTypes = ["main", "physical", "clinic"];
  type LocationType = (typeof LocationTypes)[number];

  interface Location {
    type: LocationType;
    address1: string;
    address2: string | null;
    city: string;
    state: string;
    zip: string;
  }

  interface Facility {
    name: string;
    created: Date;
    locations: Location[] | null;
  }

  const list = faker.helpers.multiple<Facility>(
    () => {
      var locations =
        Math.random() < 0.5
          ? null
          : faker.helpers.multiple<Location>(
              () => {
                var state = faker.location.state({ abbreviated: false });
                return {
                  type: faker.helpers.arrayElement(LocationTypes),
                  address1: faker.location.streetAddress(false),
                  address2:
                    Math.random() < 0.5
                      ? null
                      : faker.location.secondaryAddress(),
                  city: faker.location.city(),
                  state: state,
                  zip: faker.location.zipCode(),
                };
              },
              { count: { min: 1, max: 5 } }
            );
      return {
        name: faker.company.name(),
        created: faker.date.past({
          years: 20,
        }),
        locations: locations,
      };
    },
    { count: Math.random() * 200 + 50 }
  );
</script>

<ul>
  {#each list as item}
    <li>{item.name} ({item.created.toLocaleDateString()})</li>
  {/each}
</ul>

<style>
  ul {
    list-style: none;
    text-align: left;
    padding-left: 0;
  }
  li {
    padding: 0.25rem 0 0.25rem 0;
    margin: 0.25rem 0 0.25rem 0;
  }
</style>
