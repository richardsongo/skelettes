# skelettes
Templates


Craft Filters:


{{ some_html|striptags }}

<p>The striptags filter strips SGML/XML (HTML) tags and replace adjacent whitespace by one space </p>


<h2>Author Tags</h2>

<pre>

{{ entry.author.socialTwitter }}
{{ entry.author.socialFacebook }}
{{ entry.author.fullName }}
{{ entry.author.bio }}

</pre>



<h2>Entries except the first one</h2>

{% set entries = craft.entries.section('articles').limit(3).find %}
{% set firstEntry = entries[0] %}
{% set remainingEntries = entries|without(firstEntry) %}

<h2> 2. Conditionals </h2>
<pre>
{% if something == 'value' %}
    ...
{% elseif somethingElse == 'otherValue' %}
    ...
{% else %}
    ...
{% endif %}


{% for block in contactDetails.myMatrixField %}
     {{ block.location }}
     {{ block.address }}
{% endfor %}

{% for block in socialNetworks.socialLinks %}
{% if block.facebook %}     {{ block.facebook }}  {% endif %}
{% if block.twitter %}      {{ block.twitter }}   {% endif %}
{% if block.youtube %}      {{ block.youtube }}   {% endif %}
{% if block.instagram %}    {{ block.instagram }} {% endif %}
{% endfor %}
</pre>
<div class="highlight highlight-text-html-django">
<pre>
<ul>
<li id="facebook"><a href="#" target="_blank" alt="Facebook" title="Facebook">  <i class="fa fa-facebook"></i>   </a></li>
<li id="twitter"><a href="#" target="_blank" alt="Twitter" title="Twitter">          <i class="fa fa-twitter"></i>    </a></li>
<li id="youtube"><a href="#" target="_blank" alt="YouTube" title="YouTube"> <i class="fa fa-youtube"></i>    </a></li>
<li id="itunes"><a href="#" target="_blank" alt="iTunes" title="iTunes"> <i class="fa fa-instagram"></i> </a></li>
</ul>
 </pre>               
</div>               
  <pre>              
F	A full textual representation of a month, such as January or March
{{ entry.postDate | date("d M, Y") }}
</pre>


<h2>Is it possible to change a loop if mobile browser is detected?</h2>
<p>http://craftcms.stackexchange.com/questions/11250/is-it-possible-to-change-a-loop-if-mobile-browser-is-detected
</p>
{% if craft.request.isMobileBrowser %}
    {% for batch in craft.entries.section('afval')|batch(2) %}
        ...
    {% endfor %}
{% else %}
    {% for batch in craft.entries.section('afval')|batch(3) %}
        ...
    {% endfor %}
{% endif %}

Or 
{% set batch = craft.request.isMobileBrowser ? 2 : 3 %}

{% for batch in craft.entries.section('afval') | batch(batch) %}
    ...
{% endfor %}
