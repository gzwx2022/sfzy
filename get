// worker.js

addEventListener('fetch', event => {
  const url = 'https://skill-note.blogspot.com/2023/06/bloggerfloat_14.html';

  // Get the request
  const request = event.request;

  // Check if the request method is GET
  if (request.method === 'GET') {
    // Get the current time
    const now = new Date();
    const formattedNow = now.toLocaleString();

    // Fetch the third Google Drive link
    fetch(url)
      .then(response => response.text())
      .then(html => {
        // Parse the HTML and extract the third Google Drive link using regex
        const regex = /https:\/\/drive\.google\.com\/file\/d\/(.*?)\/view/g;
        const matches = html.matchAll(regex);

        // If a match is found, generate the HTML page
        if (matches.length >= 3) {
          const thirdDriveLink = matches[2][0];
          const nextFetchTime = new Date(now.getTime() + 24 * 60 * 60 * 1000); // Next fetch time: 24 hours later
          const formattedNextFetchTime = nextFetchTime.toLocaleString();

          const htmlResponse = `
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Google Drive Link Fetcher</title>
</head>
<body>
  <h1>Google Drive Link Fetcher</h1>
  <p>Fetch time: ${formattedNow}</p>
  <p>Third Google Drive link: <a href="${thirdDriveLink}">${thirdDriveLink}</a></p>
  <p>Next fetch time: ${formattedNextFetchTime}</p>
</body>
</html>
          `;

          event.respondWith(
            new Response(htmlResponse, {
              headers: {
                'Content-Type': 'text/html',
              },
            })
          );
        } else {
          // If no match is found, return an error message
          event.respondWith(
            new Response('Failed to fetch Google Drive link', {
              status: 500,
            })
          );
        }
      })
      .catch(error => {
        console.error('Error fetching URL:', error);
        event.respondWith(
          new Response('Failed to fetch URL', {
            status: 500,
          })
        );
      });
  } else {
    // If the request method is not GET, return the original response
    event.respondWith(new Response('Not Found', {
      status: 404,
    }));
  }
});
