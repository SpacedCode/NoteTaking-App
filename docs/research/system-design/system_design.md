<h1>System Design</h1>
In this page, we'll discuss about how our app uses some technologies and algorithms together in order to meet the system design requirements.


<h3>A. Requirements (After 1-year Assumptions)</h3>

<li>Total registered users: 2.500 users</li>
<li>Total daily users: 100 users</li>
<li>Size for one user: ~224 Bytes</li>

<pre>
      1. id (uses UUID): 16 bytes
      2. username (max 50 characters): max 50 bytes
      3. password (uses Argon2): 150 Bytes
      4. created_at (uses Datetime): 8 bytes      
</pre>
      
<li>Total size for all users: ~560 KBytes</li>

<pre>

      224 Bytes x 2.500 users
      = 560.000 Bytes
      = 560 KBytes
</pre>

<li>Size for one note: ~374 Bytes</li>
<pre>
      1. id (uses UUID): 16 bytes
      2. title (max 100 characters): max 100 bytes
      3. subtitle (max 200 characters): max 200 bytes
      4. author_name (links to user's username): max 50 bytes
      5. created_at (uses Datetime): 8 bytes
</pre> 

<li>Average notes for non-daily users: 1 note</li>
<li>Average notes for daily users: 5 notes</li>
<li>Total notes: ~2.900 notes</li>

<pre>
      1. non-daily users: 
            = 1 note x (2.500 total users - 100 daily users)
            = 1 note x (2.400 non-daily users)
            = 2.400 notes (owned by non-daily users)
      2. daily users:
            = 5 notes x 100 daily users
            = 500 notes (owned by daily users)
</pre>

<li>Total size for all notes: ~1,0846 MBytes</li>

<pre>
      374 Bytes x 2.900 notes
      = 1.084.600 Bytes
      = 1,0846 MBytes
</pre>

<li><ins>Total size for all data: ~1,6446 MBytes</ins></li>

<pre>
      all notes data + all users data
      = 1,0846 MBytes + 560 KBytes
      = 1,0846 MBytes + 0,56 MBytes
      = 1,6446 MBytes
</pre>