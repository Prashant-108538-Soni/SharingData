import 'package:flutter/material.dart';
import 'package:flutter_svg/svg.dart';

/// A customizable tertiary button widget that presents a dropdown menu of options.
/// This widget provides a button with a border that, when tapped, reveals a
/// popup menu. The menu items are dynamically generated from a list of strings
/// and a callback function handles the selection of an item.
/// It uses the application's primary color for the border.
/// The button takes a list of [options] (strings), a callback [onSelect]
/// for when an option is chosen, and a [icon] widget to display as the button itself.

class MenuButton extends StatelessWidget {
  /// The list of strings to be displayed as menu options.
  final List<String> options;

  /// The callback function executed when a menu option is selected.
  /// It receives the selected string as an argument.
  final ValueChanged<String> onSelect;

  /// The widget displayed as the button that triggers the popup menu.
  final String iconPath;

  /// Creates a tertiary button with a dropdown menu.
  const MenuButton({
    super.key,
    required this.options,
    required this.onSelect,
    required this.iconPath,
  });

  @override
  Widget build(BuildContext context) {
    return Container(
      decoration: BoxDecoration(
        border: Border.all(color: Theme.of(context).primaryColor),
        borderRadius: BorderRadius.circular(8),
      ),
      child: PopupMenuButton<String>(
        onSelected: onSelect,
        itemBuilder: (BuildContext context) {
          return options
              .map(
                (String choice) =>
                    PopupMenuItem<String>(value: choice, child: Text(choice)),
              )
              .toList();
        },
        icon: SvgPicture.asset(
          iconPath,
          // Fallback icon if asset fails to load
          placeholderBuilder: (BuildContext context) =>
          const Icon(Icons.error_outline, color: Colors.red),
        ),
        color: Colors.white, // Explicitly set popup menu background color
        padding: EdgeInsets.zero,
        // Adjust the offset to position the dropdown below the button
        offset: Offset(0, 42),
      ),
    );
  }
}


