# Barbara Scharrer · Webinar-Landingpage

Quellcode der Webinar-Landingpage, eingebunden in Webflow via jsDelivr-CDN.

## Dateien

| Datei | Zweck |
|-------|-------|
| `webflow-embed-loader.html` | Snippet für den Webflow Code-Embed (3 KB). Enthält BSLP_CONFIG + Loader. |
| `webinar-content.txt` | Vollständiges HTML/CSS/JS, das via jsDelivr nachgeladen wird (~110 KB). |
| `webinar-landingpage-embed.html` | Stand-alone Vollversion (Loader + Content kombiniert) — für lokale Tests. |
| `barbara-scharrer-bg.jpg` | Hero-Hintergrund (Yoga-Studio-Foto). |
| `barbara-scharrer-host.jpg` | „Deine Gastgeberin"-Foto (Barbara sitzend). |
| `aufrechtprinzip.png` | 3-Stadien-Skelett-Skizze für die Solution-Card. |

## Workflow

1. Lokal Änderungen am `webinar-landingpage-embed.html`
2. `webinar-content.txt` regenerieren (Helper-Script unten)
3. `git add -A && git commit -m "..." && git push`
4. jsDelivr aktualisiert sich automatisch (Cache ~ 12 h)
5. Sofortige Aktualisierung: `https://purge.jsdelivr.net/gh/directmailing-io/barbara-scharrer-webinar-lp@main/webinar-content.txt` einmalig im Browser öffnen

## jsDelivr-URLs

- Content: `https://cdn.jsdelivr.net/gh/directmailing-io/barbara-scharrer-webinar-lp@main/webinar-content.txt`
- Hero-BG: `https://cdn.jsdelivr.net/gh/directmailing-io/barbara-scharrer-webinar-lp@main/barbara-scharrer-bg.jpg`
- Host-Foto: `https://cdn.jsdelivr.net/gh/directmailing-io/barbara-scharrer-webinar-lp@main/barbara-scharrer-host.jpg`
- Aufricht: `https://cdn.jsdelivr.net/gh/directmailing-io/barbara-scharrer-webinar-lp@main/aufrechtprinzip.png`

## Content-Datei regenerieren

```bash
python3 -c "
src = open('webinar-landingpage-embed.html').read()
start = src.index('<!-- ============================================================\n     ZENTRALE KONFIG')
end_marker = '</script>\n\n<style>'
end_idx = src.index(end_marker, start)
external = src[:start] + src[end_idx + len('</script>\n\n'):]
open('webinar-content.txt', 'w').write(external)
print('written:', len(external), 'chars')
"
```
