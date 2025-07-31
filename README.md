import 'package:flutter/material.dart';

/// A reusable secondary button with an outlined style.
///
/// Typically used for medium-emphasis actions.  
/// Styled with the app’s `colorScheme.primary` for border and text color.
class SecondaryButton extends StatelessWidget {
  /// Text label displayed inside the button.
  final String title;

  /// Callback executed when the button is pressed.
  final VoidCallback onTap;

  const SecondaryButton({
    super.key,
    required this.title,
    required this.onTap,
  });

  @override
  Widget build(BuildContext context) {
    final TextStyle? buttonTextStyle = Theme.of(context).textTheme.labelLarge;

    return OutlinedButton(
      onPressed: onTap,
      style: OutlinedButton.styleFrom(
        shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(8.0)),
        side: BorderSide(color: Theme.of(context).colorScheme.primary),
      ),
      child: Text(
        title,
        style: buttonTextStyle?.copyWith(
          color: Theme.of(context).colorScheme.primary,
          fontWeight: FontWeight.bold,
        ),
      ),
    );
  }
}