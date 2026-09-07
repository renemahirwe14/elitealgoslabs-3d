# Elite Algos 3D — deployment notes
## Preview (SAFE, non-destructive)
- URL: https://elitealgoslabs.com/preview3d/
- Served by docker service `preview3d` (nginx:alpine) on `easypanel` overlay,
  bind-mounted: /home/ubuntu/.openclaw/workspace/elitealgos-3d -> /usr/share/nginx/html:ro
  (so edits to index.html here appear instantly at /preview3d/)
- Traefik route: /etc/easypanel/traefik/config/preview3d.yaml
  Host(`elitealgoslabs.com`) && PathPrefix(`/preview3d`), priority 1000, stripPrefix.
- Main site (root /) = OLD Next.js `elitealgos_web` service, UNTOUCHED.
- GitHub: renemahirwe14/elitealgoslabs-3d (public, for Pages).

## To PROMOTE to main elitealgoslabs.com (only on Rene's explicit OK)
1. Back up /etc/easypanel/traefik/config/elitealgoslabs.yaml
2. Point service `elitealgoslabs-web` to preview3d OR change root router service.
## To REMOVE preview
- sudo rm /etc/easypanel/traefik/config/preview3d.yaml ; docker service rm preview3d
