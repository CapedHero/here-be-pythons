.. _cookiecutter_yapf:


Black - The Uncompromising Formatter
====================================

.. admonition:: Main point
   :class: tip

   `Black <https://github.com/psf/black>`_'s goal is to make Python code look as good as written by a programmer who is rigorously following a style guide. It proved to be much better than any of its alternatives.

   **Make it your favorite formatter right now.**

+ Black reformats entire files in place. **It is not configurable!** Thanks to that:

    + Blackened code will look the same regardless of the project you're reading. Formatting becomes transparent after a while and you can focus on the content instead.

    + **Black makes code review much, much faster!** 🚀 It's been proven empirically on every single project it was applied.

    + All in all, you will save time and mental energy for more important matters than formatting, while keeping your code straight, beautiful and readable.

+ It is recommended to include Black in your linting Invoke task and also to run it during pre-commit Git Hook. Example of both can be found in Big-Bang-py, see `project.py <https://github.com/CapedHero/big-bang-py/blob/74aa5588584f61ad83b6a1078e00911c3cb974f5/%7B%7Bcookiecutter.project_dir%7D%7D/tasks/project.py#L36-L37>`_ and `CI checks <https://github.com/RTBHOUSE/big-bang-py/blob/master/%7B%7Bcookiecutter.project_dir%7D%7D/githooks/pre-commit#L47-L59>`_ called by `Git Hook <https://github.com/CapedHero/big-bang-py/blob/74aa5588584f61ad83b6a1078e00911c3cb974f5/%7B%7Bcookiecutter.project_dir%7D%7D/ci/ci_checks.py#L43-L54>`_.

+ To manage edge cases, `disable Black <https://github.com/psf/black#the-black-code-style>`_ per block:

    .. code-block:: python

        # fmt: off

        all_domains_dict_1 = {
            'valid-safe-foo-1.bar': {'impression': 1},
            'valid-safe-foo-2.bar': {'impression': 2},
        }

        all_domains_dict_2 = {
            'valid-safe-spam-3.eggs': {'impression': 3},
            'valid-safe-spam-4.eggs': {'impression': 4},
        }
        unsafe_domains_dict_2 = {
            'valid-unsafe-spam-1.eggs': {'impression': 5},
            'valid-unsafe-spam-2.eggs': {'impression': 6},
        }

        # fmt: on


YAPF - Google's Alternative
---------------------------

+ The formatting style used by YAPF is configurable, where specific configuration can be pointed in a couple of ways.

    + It is recommended to store the configuration in a properly formatted ``.style.yapf`` file at the root of your project.

    + You may find pre-configured ``.style.yapf`` in `Big-Bang-py <https://github.com/RTBHOUSE/big-bang-py/blob/master/%7B%7Bcookiecutter.project_dir%7D%7D/.style.yapf>`_.

+ It is recommended to include YAPF in your linting Invoke task and also to run it during pre-commit Git Hook. Example of both can be found in Big-Bang-py, see `project.py <https://github.com/RTBHOUSE/big-bang-py/blob/master/%7B%7Bcookiecutter.project_dir%7D%7D/tasks/project.py#L37-L38>`_ and `pre-commit <https://github.com/RTBHOUSE/big-bang-py/blob/master/%7B%7Bcookiecutter.project_dir%7D%7D/githooks/pre-commit#L47-L59>`_.

+ To manage edge cases, `disable YAPF <https://github.com/google/yapf#why-does-yapf-destroy-my-awesome-formatting>`_:

    + per line:

    .. code-block:: python

        INTERVALS = (
            ('weeks',   60 * 60 * 24 * 7),
            ('days',    60 * 60 * 24),
            ('hours',   60 * 60),
            ('minutes', 60),
            ('seconds', 1),
        )  # yapf: disable

    + per block:

    .. code-block:: python

        # yapf: disable

        all_domains_dict_1 = {
            'valid-safe-foo-1.bar': {'impression': 1},
            'valid-safe-foo-2.bar': {'impression': 2},
        }

        all_domains_dict_2 = {
            'valid-safe-spam-3.eggs': {'impression': 3},
            'valid-safe-spam-4.eggs': {'impression': 4},
        }
        unsafe_domains_dict_2 = {
            'valid-unsafe-spam-1.eggs': {'impression': 5},
            'valid-unsafe-spam-2.eggs': {'impression': 6},
        }

        # yapf: enable

+ Survival tips:

    + If you leave trailing comma in a collection (be it a list, function parameters, etc.), YAPF will force it to break, giving one element per line.

    + YAPF is not perfect - from time to time you WILL see weirdly formatted code. There are at least two major occurrences:

        + Deeply Nested Dicts - this is quite understandable as decisions that improve readability are usually arbitrary and should be solved on a case-by-case basis.

        + Complex Comprehensions - comprehensions are split over multiple lines only when they exceed the column limit... This issue is brought to the attention of both YAPF authors (see issue on `Github <https://github.com/google/yapf/issues/628>`_) and other programmers (see posts on `Reddit <https://www.reddit.com/r/Python/comments/9mov4r/is_there_a_way_to_force_yapf_to_always_splitfold>`_) and `Stack Overflow <https://stackoverflow.com/questions/52558919/is-there-a-way-to-force-yapf-to-always-split-fold-comprehensions>`_).

