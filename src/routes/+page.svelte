<script>
	function getSource(filename) {
		return `/profil_pictures/${filename}`;
	}
	let new_fil = 
[
  {
    id_utilisateur: 1,      
    pseudo: 'Bisquette',    
    photo: 'Bisquette.jpeg',
    date: '2023-07-10T15:52:33+02:00'
  },
  { id_utilisateur: 2, pseudo: 'Saké', photo: null, date: null },
  { id_utilisateur: 3, pseudo: 'Sakééééé', photo: null, date: null },
  { id_utilisateur: 4, pseudo: 'Biscotte', photo: null, date: null },
  { id_utilisateur: 5, pseudo: 'oui', photo: 'oui.png', date: null },
  {
    id_utilisateur: null,
    pseudo: null,
    photo: null,
    date: 'Mon Aug 13 2001 02:00:00 GMT+0200 (heure d’été d’Europe centrale)'
  }
]
[
  {
    post: {
      id_post: 10,
      texte: "j'ai trop hâte de voir le prochain Barbie",
      auteur: 1,
      photo: 'Bisquette.jpeg',
      date: '2023-06-29T14:24:43+02:00',
      type: 'Article',
      media: '',
      pseudo: 'Bisquette',
      up: 1,
      down: null,
      propreVote: 1
    },
    commentaire: [
  {
    id_commentaire_post: 14,
    contenu: 'azerty',      
    id_user: 1,
    pseudo: 'Bisquette',    
    photo: 'Bisquette.jpeg',
    date: '2023-07-10T16:10:02+02:00',
    media: '',
    up: null,
    down: null,
    propreVote: null
  },
  {
    id_commentaire_post: 13,
    contenu: 'oui',
    id_user: 1,
    pseudo: 'Bisquette',
    photo: 'Bisquette.jpeg',
    date: '2023-07-06T16:34:00+02:00',
    media: '',
    up: 1,
    down: null,
    propreVote: 1
  },
  {
    id_commentaire_post: 12,
    contenu: "moi aussi !!!! y'a Margot Robbie en plus dedans hehe",
    id_user: 3,
    pseudo: 'Sakééééé',
    photo: null,
    date: '2023-06-30T09:41:08+02:00',
    media: '',
    up: null,
    down: 1,
    propreVote: -1
  }
]
  },
  {
    post: {
      id_post: 6,
      texte: "J'aime bien le film Death Note",
      auteur: 2,
      photo: null,
      date: '2023-06-23T13:13:18+02:00',
      type: 'Débat',
      media: '',
      pseudo: 'Saké',
      up: 1,
      down: null,
      propreVote: null
    },
    commentaire: []
  },
  {
    post: {
      id_post: 2,
      texte: 'Pourquoi les gens aiment bien Tarantino ? Je ne comprends absolument rien à ces films',
      auteur: 4,
      photo: null,
      date: '2023-06-20T10:54:42+02:00',
      type: 'Article',
      media: '',
      pseudo: 'Biscotte',
      up: 1,
      down: null,
      propreVote: 1
    },
    commentaire: [
  {
    id_commentaire_post: 4,
    contenu: 'wesh ?',
    id_user: 1,
    pseudo: 'Bisquette',
    photo: 'Bisquette.jpeg',
    date: '2023-06-28T09:18:09+02:00',
    media: '',
    up: null,
    down: null,
    propreVote: null
  },
  {
    id_commentaire_post: 2,
    contenu: "Pulp Fiction est le meilleur de ses films avec une intrigue déstructuré qui transforme l'histoire en puzzle à reconstruire pièce par pièce pour former un scénario grandiose !",
    id_user: 3,
    pseudo: 'Sakééééé',
    photo: null,
    date: '2023-06-27T17:36:12+02:00',
    media: '',
    up: null,
    down: 2,
    propreVote: -1
  }
]
  }
];
</script>

<button>
	<a href="/"> Paramètres </a>
</button>
<button>
	<a href="/"> Nouveau post </a>
</button>

<form method="POST">
	<button type="submit" name="deco"> Déconnexion </button>
</form>
<div class="content">
	<h1>Fil d'actualités</h1>

	{#each new_fil as post}
		<div>
			<div>
				<form method="POST">
					{post.post.type}
					de
					<button type="submit" name="page" value={post.post.auteur}>{post.post.pseudo}</button>
					{#if !!post.post.photo}
						<img class="profil_photo" src={getSource(post.post.photo)} alt="profile_picture" />
					{:else}
						<img class="profil_photo" src="/icon/defaut_photo_profil.png" alt="profile_picture" />
					{/if}
					{post.post.date}
				</form>
			</div>
			<div>
				{post.post.texte}
			</div>

			<form method="POST">
				<div>
					{post.post.up || 0}

					<button type="submit" name="up" value={post.post.id_post}>
						{#if post.post.propreVote == 1}
							AlreadyUp
						{:else}
							Up
						{/if}
					</button>
					<button type="submit" name="down" value={post.post.id_post}>
						{#if post.post.propreVote == -1}
							AlreadyDown
						{:else}
							Down
						{/if}
					</button>

					{post.post.down || 0}
				</div>
				<div>
					<input id="comment" type="text" name="comment" />
					<button type="submit" name="post" value={post.post.id_post} />
				</div>

				{#each post.commentaire as comm}
					<div>
						-> {comm.pseudo}
						{#if !!comm.photo}
							<img class="profil_photo" src={getSource(comm.photo)} alt="profile_picture" />
						{:else}
							<img class="profil_photo" src="/icon/defaut_photo_profil.png" alt="profile_picture" />
						{/if}
						{comm.date}
					</div>
					<div>
						----- {comm.contenu}
					</div>

					<div>
						----- {comm.up || 0}

						<button type="submit" name="up_comm" value={comm.id_commentaire_post}>
							{#if comm.propreVote == 1}
								AlreadyUp
							{:else}
								Up
							{/if}
						</button>
						<button type="submit" name="down_comm" value={comm.id_commentaire_post}>
							{#if comm.propreVote == -1}
								AlreadyDown
							{:else}
								Down
							{/if}
						</button>

						{comm.down || 0}
					</div>
				{/each}
			</form>
		</div>
		<div>&nbsp;</div>
	{/each}
</div>

<style>
	.content {
		width: 100%;
		max-width: var(--column-width);
		margin: var(--column-margin-top) auto 0 auto;
	}
	.profil_photo {
		border-radius: 50%;
		width: 85px;
		height: 85px;
		object-fit: cover;
		margin-left: 10px;
		margin-right: 10px;
	}
</style>
