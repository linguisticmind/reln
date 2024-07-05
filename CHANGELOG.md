# reln changelog

<table>
    <tr>
        <th>Version</th>
        <th>Date</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>
            <a href="https://github.com/linguisticmind/reln/releases/tag/v0.1.3">0.1.3</a>
        </td>
        <td>
            2024-07-05
        </td>
        <td>
            <p>
                Fixed incorrect handling of the target argument when only two non-option arguments are passed, and the target argument is a path to a symbolic link that points to a directory. Trailing forward slash can now be used to treat such a symbolic link as a directory; otherwise, it is treated as a regular file. Without a trailing forward slash, the symbolic link will be overwritten, or <code>reln</code> will throw an error&#8203;&mdash;depending on the <code>-y, --overwrite / -Y, --no-overwrite</code> setting; if a trailing forward slash is added, a new symbolic link will be put into the directory that the symbolic link passed as the target argument to <code>reln</code> is pointing to.
            </p>
        </td>
    </tr>
    <tr>
        <td>
            <a href="https://github.com/linguisticmind/reln/releases/tag/v0.1.2">0.1.2</a>
        </td>
        <td>
            2024-06-18
        </td>
        <td>
            <p>
                Fixed incorrect handling of the target argument when only two non-option arguments are passed, and the target argument is a path to a directory that does not have a trailing forward slash.
            </p>
        </td>
    </tr>
    <tr>
        <td>
            <a href="https://github.com/linguisticmind/reln/releases/tag/v0.1.1">0.1.1</a>
        </td>
        <td>
            2024-06-09
        </td>
        <td>
            <p>
                Specified end of options (<code>--</code>) for the <code>ls</code> and <code>unlink</code> commands to prevent problems with files whose name starts with a hyphen.<br>
                Fixed processing of <code>sim_</code> colors.<br>
                Fixed an HTML error in the CHANGELOG.
            </p>
        </td>
    </tr>
    <tr>
        <td>
            <a href="https://github.com/linguisticmind/reln/releases/tag/v0.1.0">0.1.0</a>
        </td>
        <td>
            2024-05-17
        </td>
        <td>
            <p>
                Initial release.
            </p>
        </td>
    </tr>
</table>
