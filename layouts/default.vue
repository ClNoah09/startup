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
          <LinksNavLink to="/societe">Société</LinksNavLink>
          <LinksNavLink to="/equipe">Équipe</LinksNavLink>
          <LinksNavLink to="/contact">Contact</LinksNavLink>
          <LinksNavLink to="/blog">Blog</LinksNavLink>
        </template>
      </NavsNav>
    </template>

    <template #content>
      <div
        id="fonds"
        class="min-h-screen sticky bg-cover bg-[url('/public/img/challenger-se-tient-devant-illustration-effrayante-du-chateau.jpg')]"
      >
        <slot />
      </div>
    </template>

    <template #footer>
      <FootersBasic />
    </template>
  </LayoutsBase>
</template>
