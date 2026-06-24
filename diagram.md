flowchart TD

subgraph group_grp_app["App Router"]
  node_n_home["Home feed<br/>route page<br/>[page.tsx]"]
  node_n_listing_page["Listing page<br/>route page<br/>[page.tsx]"]
  node_n_trips_page["Trips<br/>route page<br/>[page.tsx]"]
  node_n_reservations_page["Reservations<br/>route page<br/>[page.tsx]"]
  node_n_properties_page["Properties<br/>route page<br/>[page.tsx]"]
  node_n_favorites_page["Favorites<br/>route page<br/>[page.tsx]"]
end

subgraph group_grp_api["API Layer"]
  node_n_listing_api["Listings API<br/>route handlers"]
  node_n_favorites_api["Favorites API<br/>route handlers<br/>[route.ts]"]
  node_n_reservations_api["Reservations API<br/>route handlers"]
  node_n_register_api["Register API<br/>route handler<br/>[route.ts]"]
end

subgraph group_grp_ui["UI System"]
  node_n_navbar["Navbar<br/>navigation UI<br/>[Navbar.tsx]"]
  node_n_listing_card["Listing card<br/>listing UI<br/>[ListingCard.tsx]"]
  node_n_listing_reservation["Reservation panel<br/>listing UI"]
  node_n_modals["Modals<br/>interaction UI"]
  node_n_hooks["UI hooks<br/>client state"]
end

subgraph group_grp_data["Data & Auth"]
  node_n_actions["Read actions<br/>server helpers"]
  node_n_prisma[("Prisma client<br/>db client<br/>[prismadb.ts]")]
  node_n_schema["Domain schema<br/>prisma schema<br/>[schema.prisma]"]
  node_n_nextauth["Auth endpoint<br/>nextauth route<br/>[[...nextauth].ts]"]
end

subgraph group_grp_shared["Shared Runtime"]
  node_n_middleware["Middleware<br/>route guard<br/>[middleware.ts]"]
  node_n_client_only["ClientOnly<br/>boundary component<br/>[ClientOnly.tsx]"]
  node_n_toaster["Toaster<br/>infra UI"]
end

node_n_home -->|"loads listings"| node_n_actions
node_n_home -->|"renders shell"| node_n_navbar
node_n_listing_page -->|"loads detail"| node_n_actions
node_n_listing_page -->|"shares card UI"| node_n_listing_card
node_n_listing_page -->|"shows booking"| node_n_listing_reservation
node_n_trips_page -->|"loads trips"| node_n_actions
node_n_reservations_page -->|"loads reservations"| node_n_actions
node_n_properties_page -->|"loads properties"| node_n_actions
node_n_favorites_page -->|"loads favorites"| node_n_actions
node_n_actions -->|"queries db"| node_n_prisma
node_n_prisma -->|"implements model"| node_n_schema
node_n_nextauth -->|"reads users"| node_n_prisma
node_n_nextauth -->|"secures routes"| node_n_middleware
node_n_register_api -->|"creates user"| node_n_prisma
node_n_listing_api -->|"mutates listings"| node_n_prisma
node_n_favorites_api -->|"toggles favorite"| node_n_prisma
node_n_reservations_api -->|"writes reservations"| node_n_prisma
node_n_navbar -->|"uses state"| node_n_hooks
node_n_navbar -->|"opens modals"| node_n_modals
node_n_modals -->|"controls flows"| node_n_hooks
node_n_listing_card -->|"favorite action"| node_n_hooks
node_n_listing_reservation -->|"browser gate"| node_n_client_only
node_n_client_only -->|"supports UX"| node_n_toaster

click node_n_home "https://github.com/kchakhalyan/airbnb-clone/blob/main/app/page.tsx"
click node_n_listing_page "https://github.com/kchakhalyan/airbnb-clone/blob/main/app/listings/[listingId]/page.tsx"
click node_n_trips_page "https://github.com/kchakhalyan/airbnb-clone/blob/main/app/trips/page.tsx"
click node_n_reservations_page "https://github.com/kchakhalyan/airbnb-clone/blob/main/app/reservations/page.tsx"
click node_n_properties_page "https://github.com/kchakhalyan/airbnb-clone/blob/main/app/properties/page.tsx"
click node_n_favorites_page "https://github.com/kchakhalyan/airbnb-clone/blob/main/app/favorites/page.tsx"
click node_n_actions "https://github.com/kchakhalyan/airbnb-clone/tree/main/app/actions"
click node_n_prisma "https://github.com/kchakhalyan/airbnb-clone/blob/main/app/libs/prismadb.ts"
click node_n_schema "https://github.com/kchakhalyan/airbnb-clone/blob/main/prisma/schema.prisma"
click node_n_nextauth "https://github.com/kchakhalyan/airbnb-clone/blob/main/pages/api/auth/[...nextauth].ts"
click node_n_middleware "https://github.com/kchakhalyan/airbnb-clone/blob/main/middleware.ts"
click node_n_listing_api "https://github.com/kchakhalyan/airbnb-clone/tree/main/app/api/listings"
click node_n_favorites_api "https://github.com/kchakhalyan/airbnb-clone/blob/main/app/api/favorites/[listingId]/route.ts"
click node_n_reservations_api "https://github.com/kchakhalyan/airbnb-clone/tree/main/app/api/reservations"
click node_n_register_api "https://github.com/kchakhalyan/airbnb-clone/blob/main/app/api/register/route.ts"
click node_n_navbar "https://github.com/kchakhalyan/airbnb-clone/blob/main/app/components/navbar/Navbar.tsx"
click node_n_listing_card "https://github.com/kchakhalyan/airbnb-clone/blob/main/app/components/listings/ListingCard.tsx"
click node_n_listing_reservation "https://github.com/kchakhalyan/airbnb-clone/blob/main/app/components/listings/ListingReservation.tsx"
click node_n_modals "https://github.com/kchakhalyan/airbnb-clone/tree/main/app/components/modals"
click node_n_hooks "https://github.com/kchakhalyan/airbnb-clone/tree/main/app/hooks"
click node_n_client_only "https://github.com/kchakhalyan/airbnb-clone/blob/main/app/components/ClientOnly.tsx"
click node_n_toaster "https://github.com/kchakhalyan/airbnb-clone/blob/main/app/providers/ToasterProvider.tsx"

classDef toneNeutral fill:#f8fafc,stroke:#334155,stroke-width:1.5px,color:#0f172a
classDef toneBlue fill:#dbeafe,stroke:#2563eb,stroke-width:1.5px,color:#172554
classDef toneAmber fill:#fef3c7,stroke:#d97706,stroke-width:1.5px,color:#78350f
classDef toneMint fill:#dcfce7,stroke:#16a34a,stroke-width:1.5px,color:#14532d
classDef toneRose fill:#ffe4e6,stroke:#e11d48,stroke-width:1.5px,color:#881337
classDef toneIndigo fill:#e0e7ff,stroke:#4f46e5,stroke-width:1.5px,color:#312e81
classDef toneTeal fill:#ccfbf1,stroke:#0f766e,stroke-width:1.5px,color:#134e4a
class node_n_home,node_n_listing_page,node_n_trips_page,node_n_reservations_page,node_n_properties_page,node_n_favorites_page toneBlue
class node_n_listing_api,node_n_favorites_api,node_n_reservations_api,node_n_register_api toneAmber
class node_n_navbar,node_n_listing_card,node_n_listing_reservation,node_n_modals,node_n_hooks toneMint
class node_n_actions,node_n_prisma,node_n_schema,node_n_nextauth toneRose
class node_n_middleware,node_n_client_only,node_n_toaster toneIndigo
