<template>
  <Head>
    <Title>LevelLoot</Title>
    <Meta name="description" content="LevelLoot" />
  </Head>
  <LayoutsBase>
    <template #navigation>
      <NavsNav>
        <template #logo>
          <TitresLogo>LevelLoot</TitresLogo>
        </template>

        <template #links>
          <LinksNavLink to="/">Accueil</LinksNavLink>
          <LinksNavLink to="/produit">Services</LinksNavLink>
          <LinksNavLink to="#">Société</LinksNavLink>
          <LinksNavLink to="#">Équipe</LinksNavLink>
          <LinksNavLink to="#">Contact</LinksNavLink>
          <LinksNavLink to="#">Blog</LinksNavLink>
        </template>
      </NavsNav>
    </template>

    <template #content>
      <slot />
    </template>

    <template #footer>
      <FootersBasic />
    </template>
  </LayoutsBase>
</template>
