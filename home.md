import os

DEFAULT_INDEX = 'Home'

def create_index():
    """ Creates an HTML index page to redirect to an MkDocs generated page. """
    html_code = \
        "<!DOCTYPE HTML>\n " \
        "<html>\n" \
        "\t<head>\n" \
        "\t\t<meta charset=\"UTF-8\">\n" \
        "\t\t<meta http-equiv=\"refresh\" content=\"1;url=%s/index.html\">\n" \
        % DEFAULT_INDEX + \
        "\t\t<script type=\"text/javascript\">\n" \
        "\t\t\twindow.location.href = \"%s/index.html\"\n" % DEFAULT_INDEX +\
        "\t\t</script>\n" \
        "\t</head>\n" \
        "\t<body>\n" \
        "\t\tIf you are not redirected automatically to the " \
        "%s page, follow this <a href=\"%s/index.html\">link</a>\n"\
        % (DEFAULT_INDEX, DEFAULT_INDEX) + \
        "\t</body>\n" \
        "</html>\n"

    print("Creating the index.html file...\n")
    generated_site_dir = os.path.join(MKDOCS_DIR, "site", "index.html")
    index_file = open(generated_site_dir, "w")
    index_file.write(html_code)
    index_file.close()